import Button from "../../components/ui/button/Button";
import { Modal } from "../../components/ui/modal";
import { useModal } from "../../hooks/useModal";
import { useState, useEffect } from "react"; 
import {
  Table,
  TableBody,
  TableCell,
  TableHeader,
  TableRow,
} from "../../components/ui/table";
import { SearchIcon } from "../../icons";
import axios from "axios";

type SortKey =
  | "Client Name"
  | "country"
  | "Location"
  | "Contact Person Name"
  | "Email"
  | "Postal_Code";
type SortOrder = "asc" | "desc";

type ClientData = {
    [x: string]: ReactNode;
  client_name: string,
    location: string,
    country: string,
    primary_contact_name: string,
    contact_email: string,
    phone_number: string,
    Notes: string,
    address1: string,
    address2: string,
    city: string,
    state: string,
    country_id: string,
    postal_code: string,
    landmark: string,
    google_map_url: string,
    notes : string;
    
};



export default function ClientInformation() {
  const [formData, setFormData] = useState<ClientData>({
    client_name: "",
    location: "",
    country: "",
    primary_contact_name: "",
    contact_email: "",
    phone_number: "",
    Notes: "",
    address1: "",
    address2: "",
    city: "",
    state: "",
    country_id: "",
    postal_code: "",
    landmark: "",
    google_map_url: "",
    notes : ""
  });
  const [clientProfile, setClientProfile] = useState<ClientData[]>([]); 
  const { isOpen, openModal, closeModal } = useModal();
  const [sortKey, setSortKey] = useState<SortKey>("Client Name");
  const [sortOrder, setSortOrder] = useState<SortOrder>("asc");
  const [searchTerm, setSearchTerm] = useState("");
  const key = localStorage.getItem('authToken');

  useEffect(() => {
    fetchClients();
  }, []); 

  const fetchClients = async () => {
    try {
      const response = await fetch("https://abhirebackend.onrender.com/clients/clients");
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      const data = await response.json();
      setClientProfile(data);
    } catch (error) {
      console.error("Error fetching clients:", error);
      alert("Failed to fetch client data.");
    }
  };

  const handleSort = (key: SortKey) => {
    if (sortKey === key) {
      setSortOrder(sortOrder === "asc" ? "desc" : "asc");
    } else {
      setSortKey(key);
      setSortOrder("asc");
    }
  };

  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const addToList = async () => {
    if (!formData.client_name || !formData.location || !formData.country) {
      alert("Please fill all required fields: Client Name, Location, and Country.");
      return;
    }

   
    const postData = {
      client_name: formData.client_name,
      location: formData.location,
      primary_contact_name: formData.primary_contact_name,
      contact_email: formData.contact_email,
      phone_number: formData.phone_number,
      address1: formData.address1,
      address2: formData.address2,
      city: formData.city,
      state: formData.state,
      country_id:  '91',
      postal_code: formData.postal_code,
      landmark: formData.landmark,
      google_map_url: formData.google_map_url,
      notes: formData.Notes,
    };

    try {
      const response = await axios("https://abhirebackend.onrender.com/clients/clients", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Accept": "application/json",
        },
        body: JSON.stringify(postData),
      });

      if (!response) {
        throw new Error(`HTTP error! status: ${response}`);
      }
      await fetchClients();
      setFormData({
        client_name: "",
        location: "",
        country: "",
        primary_contact_name: "",
        contact_email: "",
        phone_number: "",
        Notes: "",
        address1: "",
        address2: "",
        city: "",
        state: "",
        country_id: "",
        postal_code: "",
        landmark: "",
        google_map_url: "",
        notes : ""
      });
      closeModal();
    } catch (error) {
        console.log(postData)
      console.error("Error adding client:", error);
      alert("Failed to add client. Please try again.");
    }
  };

  const filteredClients = clientProfile.filter((client: ClientData) =>
    Object.values(client).join(" ").toLowerCase().includes(searchTerm.toLocaleLowerCase())
  );

  return (
    <div>
      <div className="flex flex-between flex-wrap lg:w-[100%]">
        <div className="bg-white dark:bg-white/[0.03] mt-6 p-6 rounded-xl shadow-md w-full lg:w-[100%]">
          <h4 className="text-lg font-semibold mb-4">Client Information</h4>
          <div className="flex dark:border-white/[0.05] rounded-t-xl sm:flex-row sm:items-center sm:justify-end">
            <Button variant="outline" size="sm" onClick={openModal}>
              Add New Clients
            </Button>
          </div>
          <div className="flex py-4 flex-col dark:border-white/[0.05] rounded-t-xl sm:flex-row sm:items-center sm:justify-end">
            <div className="relative">
              <SearchIcon className="absolute text-gray-500 -translate-y-1/2 pointer-events-none left-4 top-1/2 dark:text-gray-400" />
              <input
                type="text"
                value={searchTerm}
                onChange={(e) => setSearchTerm(e.target.value)}
                placeholder="Search..."
                className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
              />
            </div>
          </div>
          <div className="w-full lg:w-[100%]">
            <Table>
              <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
                <TableRow>
                  {[
                    "Client Name",
                    "country",
                    "Location",
                    "Contact Person Name",
                    "Email",
                    "contact phone",
                    "Notes",
                    "Address1",
                    "Address2",
                    "City",
                    "State",
                    "Postal_code",
                    "Landmark",
                    "Maps_Url",
                  ].map((label, index) => (
                    <TableCell
                      key={index}
                      isHeader
                      className="px-4 py-3 border border-gray-300 dark:border-white/[0.05]"
                    >
                      <div
                        className="flex items-center justify-between cursor-pointer"
                        onClick={() =>
                          handleSort(
                            // Corrected mapping for sort keys
                            [
                              "Client Name",
                              "country",
                              "Location",
                              "Contact Person Name",
                              "Email",
                              "contact phone",
                              "Notes",
                              "Address1",
                              "Address2",
                              "City",
                              "State",
                              "Postal_Code",
                              "Landmark",
                              "Maps_Url",
                            ][index] as SortKey
                          )
                        }
                      >
                        <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                          {label}
                        </p>
                        <button className="flex flex-col gap-0.5">
                          <svg
                            className={`text-gray-300 dark:text-gray-700 ${
                              sortKey ===
                                [
                                  "Client Name",
                                  "country",
                                  "Location",
                                  "Contact Person Name",
                                  "Email",
                                  "contact phone",
                                  "Notes",
                                  "Address1",
                                  "Address2",
                                  "City",
                                  "State",
                                  "Postal_Code",
                                  "Landmark",
                                  "Maps_Url",
                                ][index] && sortOrder === "asc"
                                ? "text-brand-500"
                                : ""
                            }`}
                            width="8"
                            height="5"
                            viewBox="0 0 8 5"
                            fill="none"
                          >
                            <path
                              d="M4.40962 0.585167C4.21057 0.300808 3.78943 0.300807 3.59038 0.585166L1.05071 4.21327C0.81874 4.54466 1.05582 5 1.46033 5H6.53967C6.94418 5 7.18126 4.54466 6.94929 4.21327L4.40962 0.585167Z"
                              fill="currentColor"
                            />
                          </svg>
                          <svg
                            className="text-gray-300 dark:text-gray-700"
                            width="8"
                            height="5"
                            viewBox="0 0 8 5"
                            fill="none"
                          >
                            <path
                              d="M4.40962 4.41483C4.21057 4.69919 3.78943 4.69919 3.59038 4.41483L1.05071 0.786732C0.81874 0.455343 1.05582 0 1.46033 0H6.53967C6.94418 0 7.18126 0.455342 6.94929 0.786731L4.40962 4.41483Z"
                              fill="currentColor"
                            />
                          </svg>
                        </button>
                      </div>
                    </TableCell>
                  ))}
                </TableRow>
              </TableHeader>
              <TableBody className="text-center">
                {filteredClients.map((data, index) => (
                  <TableRow key={index}>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.client_name}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.country}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.location}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.Contact_Person_Name}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.email}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.contact_phone}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.Notes}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.address1}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.address2}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.city}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.state}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.postal_code}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.landmark}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.google_map_url}
                    </TableCell>
                  </TableRow>
                ))}
              </TableBody>
            </Table>
          </div>
        </div>
      </div>
      <Modal isOpen={isOpen} onClose={closeModal} className="modal-style pl-7 pt-20 pb-10 ">
        <div className="overflow-hidden ml-4">
          <div className="flex flex-col flex-3 mr-4">
            <div>
              <h2>Basic Informaion</h2>
              <div className="relative flex gap-5 mt-4">
                <div>
                  <label className="block font-medium mb-1">
                    Client Name <span style={{ color: "red" }}>*</span>
                  </label>
                  <input
                    type="text"
                    placeholder="Field Name"
                    value={formData.client_name}
                    name="client_name"
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                  />
                </div>
                <div>
                  <label className="block font-medium mb-1">
                    Client Location <span style={{ color: "red" }}>*</span>
                  </label>
                  <input
                    type="text"
                    placeholder="Location"
                    value={formData.location}
                    name="location"
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                  />
                </div>
              </div>
              <div className="flex gap-5 mt-4">
                <div>
                  <label className="block font-medium mb-1">
                    Contact Person Name <span style={{ color: "red" }}>*</span>
                  </label>
                  <input
                    type="text"
                    placeholder="Contact_Person_Name"
                    value={formData.Contact_Person_Name}
                    name="Contact_Person_Name"
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    required
                  />
                </div>
                <div>
                  <label className="block font-medium mb-1">
                    Contact Email <span style={{ color: "red" }}>*</span>
                  </label>
                  <input
                    type="text"
                    placeholder="Email"
                    name="email"
                    value={formData.email}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                  />
                </div>
              </div>
              <div className="flex gap-4 mt-4">
                <div>
                  <label className="block font-medium mb-1">Contact phone</label>
                  <input
                    type="Number"
                    placeholder="Phone"
                    name="phone_number"
                    value={formData.phone_number}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                  />
                </div>
                <div>
                  <label className="block font-medium mb-1">Notes</label>
                  <input
                    type="text"
                    placeholder="Notes"
                    name="Notes"
                    value={formData.Notes}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                  />
                </div>
              </div>
              <div className="mt-5 mb-4">
                <h2>Location</h2>
                <div className="flex gap-5 mt-1">
                  <div>
                    <label className="block font-medium mb-1">
                      Address1 <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="Address1"
                      name="address1"
                      value={formData.address1}
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                  <div>
                    <label className="block font-medium mb-1">
                      Address2 <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="address2"
                      value={formData.address2}
                      name="address2"
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                </div>
                <div className="flex gap-5 mt-2">
                  <div>
                    <label className="block font-medium mb-1">
                      City <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="city"
                      name="city"
                      value={formData.city}
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                  <div>
                    <label className="block font-medium mb-1">
                      State <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="state"
                      value={formData.state}
                      name="state"
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                </div>
                <div className="flex gap-5 mt-2">
                  <div className="col-span-2 lg:col-span-1">
                    <label className="block font-medium mb-1">
                      country <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="country"
                      value={formData.country}
                      name="country"
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                  <div>
                    <label className="block font-medium mb-1">
                      Postal Code <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="Postal Code"
                      value={formData.postal_code}
                      name="postal_code"
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                </div>
                <div className="flex gap-5 mt-3">
                  <div>
                    <label className="block font-medium mb-1">
                      LandMark <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="landmark"
                      name="landmark"
                      value={formData.landmark}
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                  <div>
                    <label className="block font-medium mb-1">
                      Google Map Url <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="Google Map Url"
                      value={formData.google_map_url}
                      name="google_map_url"
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                </div>
              </div>
              <div className="relative justify-end flex mt-5 gap-5 mr-5 ">
                <Button onClick={closeModal}> Close </Button>
                <Button onClick={addToList}> Save </Button>
              </div>
            </div>
          </div>
        </div>
      </Modal>
    </div>
  );
}

Clientinformation.tsx:129 
 POST https://abhirebackend.onrender.com/clients/clients 403 (Forbidden)
Clientinformation.tsx:162 
{client_name: '@!@qw123', location: '1234@#$%', primary_contact_name: '', contact_email: '', phone_number: '1234567890', …}
Clientinformation.tsx:163 Error adding client: 
AxiosError {message: 'Request failed with status code 403', name: 'AxiosError', code: 'ERR_BAD_REQUEST', config: {…}, request: XMLHttpRequest, …}
code
: 
"ERR_BAD_REQUEST"
config
: 
{transitional: {…}, adapter: Array(3), transformRequest: Array(1), transformResponse: Array(1), timeout: 0, …}
message
: 
"Request failed with status code 403"
name
: 
"AxiosError"
request
: 
XMLHttpRequest {onreadystatechange: null, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, …}
response
: 
{data: {…}, status: 403, statusText: '', headers: AxiosHeaders, config: {…}, …}
status
: 
403
stack
: 
"AxiosError: Request failed with status code 403\n    at settle (http://localhost:5173/node_modules/.vite/deps/axios.js?v=fc744e7a:1218:12)\n    at XMLHttpRequest.onloadend (http://localhost:5173/node_modules/.vite/deps/axios.js?v=fc744e7a:1550:7)\n    at Axios.request (http://localhost:5173/node_modules/.vite/deps/axios.js?v=fc744e7a:2108:41)\n    at async addToList (http://localhost:5173/src/pages/CompanyProfile/Clientinformation.tsx?t=1749526573388:96:30)"
[[Prototype]]
: 
Error
