<Modal isOpen={isOpen} onClose={closeModal} className="modal-style w-full w-[100px] pl-40 pr-40">
        <div className="no-scrollbar relative w-full w-[700vw] overflow-y-auto rounded-3xl bg-white p-4 dark:bg-gray-900 ">
            <div className="overflow-hidden  rounded-2xl bg-white dark:bg-white/[0.03] border border-gray-200 dark:border-gray-800">
            <div className="flex flex-col gap-4 px-4 py-4 border border-b-0 border-gray-100 dark:border-white/[0.05] rounded-t-xl sm:flex-row sm:items-center sm:justify-between">
                    <div className="pl-10">
                    <h3 className="text-base font-medium text-gray-800 dark:text-white/90">
                        Address Fields Configuration
                    </h3>
                    <div className="relative flex gap-5 mt-4">
                         <div>
                    <label className="block font-medium mb-1">Address 1</label>
                     <input
                    type="text"
                    placeholder="Field Name"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                /> 
                </div>
                <div>
                <label className="block font-medium mb-1">Address 2</label>
                <input
                    type="text"
                    placeholder="Description"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               <div>
                <label className="block font-medium mb-1">Land Mark</label>
                <input
                    type="text"
                    placeholder="Description"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               <div>
                <label className="block font-medium mb-1">City</label>
                <input
                    type="text"
                    placeholder="Description"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               </div>
               <div className="flex gap-5 mt-4">
                <div>
                <label className="block font-medium mb-1">State</label>
                <input
                    type="text"
                    placeholder="Description"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               <div>
                <label className="block font-medium mb-1">Postal Code</label>
                <input
                    type="text"
                    placeholder="Description"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               <div>
                <label className="block font-medium mb-1">Country</label>
                <input
                    type="text"
                    placeholder="Description"
                    className="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent py-2.5 pl-11 pr-4 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800 xl:w-[300px]"
                />
               </div>
               <div>
                <label className="block font-medium mb-1">Google Maps</label>
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
                                    {[
                                      { key: "address_1", label: "Address 1" },
                                      { key: "address_2", label: "Address 2" },
                                      { key: "landmark", label: "Land Mark" },
                                      { key: "city", label: "City" },
                                      { key: "state", label: "State" },
                                      { key: "postal_code", label: "Postal Code" },
                                      { key: "country", label: "Country" },
                                      { key: "google_maps", label: "Google Maps" }
                                    ].map(({ key, label }) => (
                                      <TableCell
                                        key={key}
                                        isHeader
                                        className="px-4 py-3 border border-gray-300 dark:border-white/[0.05]"
                                      >
                                        <div
                                          className="flex items-center justify-between cursor-pointer"
                                        >
                                          <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                                            {label}
                                          </p>
                                        </div>
                                      </TableCell>
                                    ))}
                                  </TableRow>
                            </TableHeader>
                            <TableBody>
                            <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap" children={undefined}>
                            </TableCell>
                            <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
                            </TableCell>
                            <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
                            </TableCell>
                            <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
                            </TableCell>
                            <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
                            </TableCell>
                            <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
                            </TableCell>
                            <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
                            </TableCell>
                            <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-300 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap " children={undefined}>
                            </TableCell>
                            </TableBody>
                            </Table>
                        </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        </Modal>
