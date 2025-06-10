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
import Select from "../../components/form/Select";
import { Controller, useForm } from "react-hook-form";
import axios from "axios"; 

type SortKey =
  | "client_name" 
  | "country"
  | "location"
  | "primary_contact_name" 
  | "contact_email" 
  | "phone_number" 
  | "notes" 
  | "address1"
  | "address2"
  | "city"
  | "state"
  | "postal_code"
  | "landmark"
  | "google_map_url"; 
type SortOrder = "asc" | "desc";

type ClientData = {
  client_name: string;
  location: string;
  country: string; 
  primary_contact_name: string; 
  contact_email: string; 
  phone_number: string;
  notes: string; 
  address1: string;
  address2: string;
  city: string;
  state: string;
  country_id: number; 
  postal_code: string;
  landmark: string;
  google_map_url: string;
  
};

export default function ClientInformation() {
  const [formData, setFormData] = useState<ClientData>({
    client_name: "",
    location: "",
    country: "", 
    primary_contact_name: "",
    contact_email: "",
    phone_number: "",
    notes: "", 
    address1: "",
    address2: "",
    city: "",
    state: "",
    country_id: 91, 
    postal_code: "",
    landmark: "",
    google_map_url: "",
  });
  const [clientProfile, setClientProfile] = useState<ClientData[]>([]);
  const [countrycodes, setcountrycode] = useState<ClientData[]>([]);
  const { isOpen, openModal, closeModal } = useModal();
  const [sortKey, setSortKey] = useState<SortKey>("client_name"); 
  const [sortOrder, setSortOrder] = useState<SortOrder>("asc");
  const [searchTerm, setSearchTerm] = useState("");
  const authToken = localStorage.getItem("authToken"); 

  useEffect(() => {
    fetchClients();
    fetchCountrycodes();
  }, []);

  const fetchClients = async () => {
    try {
      
      const response = await axios.get("https://abhirebackend.onrender.com/clients/clients", {
        headers: {
          Authorization: `Bearer ${authToken}`,
          "Content-Type": "application/json",
        },
      });
      const data: ClientData[] = response.data;
      setClientProfile(data);
    } catch (error) {
      console.error("Error fetching clients:", error);
      if (axios.isAxiosError(error) && error.response) {
        console.error("Fetch Error Response:", error.response.data);
        alert(`Failed to fetch client data: ${error.response.statusText || 'Unknown error'}. Please check your authentication.`);
      } else {
        alert("Failed to fetch client data. Please try again.");
      }
    }
  };

  const fetchCountrycodes = async () => {
     try {
      const response = await axios.get("https://abhirebackend.onrender.com/metadata/countries", {
        headers: {
          Authorization: `Bearer ${authToken}`,
          "Content-Type": "application/json",
        },
      });
      const data: ClientData[] = response.data;
      console.log(data)
      setcountrycode(data);
    } catch (error) {
      console.error("Error fetching", error);
      if (axios.isAxiosError(error) && error.response) {
        console.error("Fetch Error Response:", error.response.data);
        alert(`Failed to fetch`);
      } else {
        alert("Failed to fetch");
      }
    }
  }

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
    if (!formData.client_name || !formData.location || !formData.country_id) {
      alert("Please fill all required fields: Client Name, Location, and Country.");
      return;
    }
    if (!formData.primary_contact_name || !formData.contact_email) {
      alert("Contact Person Name and Contact Email are required.");
      return;
    }
    if (!formData.address1 || !formData.address2 || !formData.city || !formData.state || !formData.postal_code || !formData.landmark || !formData.google_map_url) {
      alert("All address and map URL fields are required.");
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
      country_id: 91,
      postal_code: formData.postal_code,
      landmark: formData.landmark,
      google_map_url: formData.google_map_url,
      notes: formData.notes, 
    };

    try {
      const response = await axios.post(
        "https://abhirebackend.onrender.com/clients/clients",
        postData,
        {
          headers: {
            Authorization: `Bearer ${authToken}`,
            "Content-Type": "application/json",
            "Accept": "application/json",
          },
        }
      );
      console.log("Client added successfully:", response.data);

      await fetchClients(); 
      setFormData({
        client_name: "",
        location: "",
        country: "",
        primary_contact_name: "",
        contact_email: "",
        phone_number: "",
        notes: "",
        address1: "",
        address2: "",
        city: "",
        state: "",
        country_id: "91", // Reset to default hardcoded ID
        postal_code: "",
        landmark: "",
        google_map_url: "",
      });
      closeModal();
    } catch (error) {
      console.log("POST Data being sent:", postData); 
      console.error("Error adding client:", error);
      if (axios.isAxiosError(error) && error.response) {
        console.error("Error Response Data:", error.response.data);
        alert(`Failed to add client`);
      } else {
        alert("Failed to add client");
      }
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
                    "Country", // Display label
                    "Location",
                    "Contact Person Name",
                    "Email",
                    "Contact Phone", // Display label
                    "Notes",
                    "Address1",
                    "Address2",
                    "City",
                    "State",
                    "Postal Code", // Display label
                    "Landmark",
                    "Maps URL", // Display label
                  ].map((label, index) => (
                    <TableCell
                      key={index}
                      isHeader
                      className="px-4 py-3 border border-gray-300 dark:border-white/[0.05]"
                    >
                      <div
                        className="flex items-center justify-between cursor-pointer"
                        // Map display labels to actual sort keys from ClientData
                        onClick={() =>
                          handleSort(
                            [
                              "client_name",
                              "country", // Assuming you'd sort by the country string here, or client_id if that were available
                              "location",
                              "primary_contact_name",
                              "contact_email",
                              "phone_number",
                              "notes",
                              "address1",
                              "address2",
                              "city",
                              "state",
                              "postal_code",
                              "landmark",
                              "google_map_url",
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
                                  "client_name",
                                  "country",
                                  "location",
                                  "primary_contact_name",
                                  "contact_email",
                                  "phone_number",
                                  "notes",
                                  "address1",
                                  "address2",
                                  "city",
                                  "state",
                                  "postal_code",
                                  "landmark",
                                  "google_map_url",
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
                      {data.country} {/* Display `country` from fetched data */}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.location}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.primary_contact_name} {/* Use correct key */}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.contact_email} {/* Use correct key */}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.phone_number}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                      {data.notes} {/* Use correct key */}
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
                      {data.google_map_url} {/* Use correct key */}
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
              <h2>Basic Information</h2> {/* Corrected spelling */}
              <div className="relative flex gap-5 mt-4">
                <div>
                  <label className="block font-medium mb-1">
                    Client Name <span style={{ color: "red" }}>*</span>
                  </label>
                  <input
                    type="text"
                    placeholder="Field Name"
                    value={formData.client_name}
                    name="client_name" // Use consistent lowercase
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
                    name="location" // Use consistent lowercase
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
                    placeholder="Contact Person Name"
                    value={formData.primary_contact_name}
                    name="primary_contact_name" // Use consistent lowercase
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
                    name="contact_email" // Use consistent lowercase
                    value={formData.contact_email}
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
                    name="phone_number" // Use consistent lowercase
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
                    name="notes" // Use consistent lowercase
                    value={formData.notes}
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
                      name="address1" // Use consistent lowercase
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
                      placeholder="Address2"
                      value={formData.address2}
                      name="address2" // Use consistent lowercase
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
                      placeholder="City"
                      name="city" // Use consistent lowercase
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
                      placeholder="State"
                      value={formData.state}
                      name="state" // Use consistent lowercase
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                </div>
                <div className="flex gap-5 mt-2">
                  <div className="col-span-2 lg:col-span-1">
                    <label className="block font-medium mb-1">
                      Country <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="Country"
                      value={formData.country} // Still using formData.country for display
                      name="country"
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                    {/* Assuming country_id is handled internally or from another source,
                        or you might need a hidden input for it if not directly from a dropdown
                        <input type="hidden" name="country_id" value={formData.country_id} />
                    */}
                  </div>
                  <div>
                    <label className="block font-medium mb-1">
                      Postal Code <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="Postal Code"
                      value={formData.postal_code}
                      name="postal_code" // Use consistent lowercase
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                </div>
                <div className="flex gap-5 mt-3">
                  <div>
                    <label className="block font-medium mb-1">
                      Landmark <span style={{ color: "red" }}>*</span>
                    </label>
                    <input
                      type="text"
                      placeholder="Landmark"
                      name="landmark" // Use consistent lowercase
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
                      name="google_map_url" // Use consistent lowercase
                      onChange={handleChange}
                      className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-4 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                    />
                  </div>
                </div>
              </div>
              <div className="relative justify-end flex mt-5 gap-5 mr-5 ">
                <Button onClick={closeModal} type="button">
                  {" "}
                  Close{" "}
                </Button>
                <Button onClick={addToList} type="submit">
                  {" "}
                  Save{" "}
                </Button>
              </div>
            </div>
          </div>
        </div>
      </Modal>
    </div>
  );
}
