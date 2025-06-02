import {
  Table,
  TableBody,
  TableCell,
  TableHeader,
  TableRow
} from "../../components/ui/table";
import Button from "../../components/ui/button/Button";
import Checkbox from "../../components/form/input/Checkbox";
import {
  PencilIcon
} from "../../icons";

export default function Companyaddress() {
    return (
        <div className="flex gap-20">
        <div className="overflow-hidden rounded-2xl bg-white dark:bg-white/[0.03] border border-gray-200 dark:border-gray-800 ml-[-6vw] lg:w-[59%] mt-5 mr-[5vw]">
                <div className="flex flex-col gap-4 px-4 py-4 border border-b-0 border-gray-100 dark:border-white/[0.05] rounded-t-xl sm:flex-row sm:items-center sm:justify-between">
                    <div>
                    <h3 className="text-base font-medium text-gray-800 dark:text-white/90">
                        Address Fields Configuration
                    </h3>
                    <div className="relative flex gap-5 mt-4">
                         <div>
                    <label className="block font-medium mb-1">Field Name</label>
                     <input
                    type="text"
                    placeholder="Field Name"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                /> 
                </div>
               <div>
                <label className="block font-medium mb-1">Description</label>
                <input
                    type="text"
                    placeholder="Description"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />

               </div>
                
                </div>
                <div className="flex mt-5">
                    <Button>+ Add Field</Button> 
                </div>
                   <div className="max-w-full overflow-x-auto custom-scrollbar mt-5">
                    <div>
                <Table>
                    <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
                    <TableRow>
                        <TableCell
                        isHeader
                  className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
                >
                  <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                    Field Name
                  </p>
                </TableCell>
                <TableCell
                  isHeader
                  className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
                >
                  <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                    Description
                  </p>
                </TableCell>
                <TableCell
                  isHeader
                  className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
                >
                  <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                    Icon
                  </p>
                </TableCell>
                <TableCell
                  isHeader
                  className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
                >
                  <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                    Action
                  </p>
                </TableCell>
              </TableRow>
            </TableHeader>
            <TableBody>
               <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                <div className="flex justify-center">
                    <Checkbox onChange={() => { } } />
                      </div>
               </TableCell>
               <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
               </TableCell>
               <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
               </TableCell>
               <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                <PencilIcon className="size-5" />
                </TableCell>
                </TableBody>
            </Table>
                </div>
            </div>
                </div>
            </div>
        </div>
    </div>
    );
}



