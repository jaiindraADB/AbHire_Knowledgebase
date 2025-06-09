
import Button from "../../components/ui/button/Button";
import { Modal } from "../../components/ui/modal";
import { useModal } from "../../hooks/useModal";
import { useState } from "react";
import {
  Table,
  TableBody,
  TableCell,
  TableHeader,
  TableRow
} from "../../components/ui/table";
import { SearchIcon } from "../../icons";

type SortKey =
  | "Client Name"
  |  "country"
  | "Location"
  |  "Time Zone"
  | "Contact Person Name"
  | "Email"

export default function ClientInformation({
    handleSearchStringChange,
    searchTerm
}:{
     handleSearchStringChange: (filter_key: string, value: string) => void;
     searchTerm: string;
}) {
    const [formData, setFormData] = useState({
                Client_Name: "",
                Location: "",
                country: "",
                Time_Zone: "",
                Contact_Person_Name: "",
                Email: "",
                contact_phone: "",
                Notes: "",
});
   const [clientProfile, setClientProfile] = useState([]);
   const { isOpen, openModal, closeModal } = useModal();
  const [sortKey, setSortKey] = useState<SortKey>("Company");
    const [sortOrder, setSortOrder] = useState<SortOrder>("asc");
  const handleSort = (key: SortKey) => {
    if (sortKey === key) {
      setSortOrder(sortOrder === "asc" ? "desc" : "asc");
    } else {
      setSortKey(key);
      setSortOrder("asc");
    }
  };
  
const handleChange = (e) => {
  setFormData({ ...formData, [e.target.name]: e.target.value });
};
const adddTolist = () => {
  if (!formData.Client_Name || !formData.Location || !formData.country) {
    alert("Please fill all required fields.");
    return;
  }

  setClientProfile([...clientProfile, formData]);
  setFormData({
    Client_Name: "",
    Location: "",
    country: "",
    Time_Zone: "",
    Contact_Person_Name: "",
    Email: "",
    contact_phone: "",
    Notes: "",
  });
  closeModal();
};
    return (
        <div>
            <div className="flex px-1 dark:border-white/[0.05] rounded-t-xl sm:flex-row sm:items-center sm:justify-end">
            <Button
            variant="outline"
            size="sm"
            onClick={openModal}
                >
            Add New Clients
            </Button>
            </div>
            <div className="flex flex-between flex-wrap lg:w-[100%]">
                <div className="bg-white dark:bg-white/[0.03] mt-6 p-6 rounded-xl shadow-md w-full lg:w-[100%]">
                <h4 className="text-lg font-semibold mb-4">Client Information</h4>
                <div className="flex px-1 py-4  dark:border-white/[0.05] rounded-t-xl sm:flex-row sm:items-center sm:justify-end">
                <div className="relative">
                <SearchIcon className="absolute text-gray-500 -translate-y-1/2 pointer-events-none left-4 top-1/2 dark:text-gray-400" />
                <input
                    type="text"
                    value={searchTerm}
                    onChange={(e) =>
                    handleSearchStringChange("job_title", e.target.value)
                    }
                    placeholder="Search..."
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
                </div>
            </div>
                <Table>
                <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
                <TableRow>
                    {[
                    "Client Name",
                    "country",
                    "Location",
                    "Time Zone",
                    "Contact Person Name",
                    "Email",
                    "contact phone",
                    'Notes'
                    ].map((label, index) => (
                    <TableCell
                            key={index}
                            isHeader
                            className="px-4 py-3 border border-gray-300 dark:border-white/[0.05]">
                            <div
                        className="flex items-center justify-between cursor-pointer"
                        onClick={() =>
                            handleSort([
                            "company",
                            "Title",
                            "start_date",
                            "end_date",
                            "is_current",
                            "duration_in_months",
                            ][index] as SortKey)
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
                                    "company",
                                    "Title",
                                    "start_date",
                                    "end_date",
                                    "is_current",
                                    "duration_in_months",
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
                {clientProfile.map((data,index) => (
                    <TableRow key={index}>
                            <TableCell  className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                                {data.Client_Name}
                            </TableCell>
                            <TableCell  className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                                {data.country}
                            </TableCell>
                            <TableCell  className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                                {data.Location}
                            </TableCell>
                            <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                                {data.Time_Zone}
                            </TableCell>
                            <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                                {data.Contact_Person_Name}
                            </TableCell>
                            <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                                {data.Email}
                            </TableCell>
                            <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                                {data.contact_phone}
                            </TableCell>
                            <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                                {data.Notes}
                            </TableCell>
                        </TableRow>
                ))}
                </TableBody>
            </Table>
            </div>
            </div>
            <Modal isOpen={isOpen} onClose={closeModal} className="modal-style pl-7 pt-20 pb-10 ">
                <div className="overflow-hidden ml-4">
                <div className="flex flex-col flex-3 mr-4">
                <div>
               <div className="relative flex gap-5 mt-4">
                         <div>
                    <label className="block font-medium mb-1">Client Name <span style={{ color: 'red' }}>*</span></label>
                    <input
                    type="text"
                    placeholder="Field Name"
                    value={formData.Client_Name}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                /> 
                </div>
                <div>
                <label className="block font-medium mb-1">Location  <span style={{ color: 'red' }}>*</span></label>
                <input
                    type="text"
                    placeholder="Location"
                    value={formData.Client_Name}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               </div>
                <div className="flex gap-5">
                    <div>
                <label className="block font-medium mb-1">Country  <span style={{ color: 'red' }}>*</span></label>
                <input
                    type="text"
                    placeholder="Country"
                    value={formData.Client_Name}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               <div>
                <label className="block font-medium mb-1">Timze Zone  <span style={{ color: 'red' }}>*</span></label>
                <input
                    type="text"
                    placeholder="Time Zone"
                    value={formData.Client_Name}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
                </div>
               <div className="flex gap-5 mt-4">
                <div>
                <label className="block font-medium mb-1">Contact Person Name  <span style={{ color: 'red' }}>*</span></label>
                <input
                    type="text"
                    placeholder="Contact Person Name"
                    value={formData.Client_Name}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                required/>
               </div>
               <div>
                <label className="block font-medium mb-1">Contact Email  <span style={{ color: 'red' }}>*</span></label>
                <input
                    type="text"
                    placeholder="Email"
                    value={formData.Client_Name}
                    onChange={handleChange}
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               </div>
               <div className="flex gap-4 mt-4">
                 <div>
                <label className="block font-medium mb-1">Contact phone</label>
                <input
                    type="text"
                    placeholder="Phone"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               <div>
                <label className="block font-medium mb-1">Notes</label>
                <input
                    type="text"
                    placeholder="Notes"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               
                </div>
               </div>
                <div className="flex mt-5 ">
                <Button onClick={adddTolist}> save </Button> 
                </div>
                </div>
                </div>
                </div>
            </Modal>
        </div>
    );
}




