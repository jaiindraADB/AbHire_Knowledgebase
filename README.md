<div className="max-w-full overflow-x-auto custom-scrollbar flex justify-center">
        <div className="card bg-white ml-3 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[48%] lg:h-[20%] ">
        <Table>
          <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
          <TableRow>
            <TableCell isHeader children={undefined} />
           {[
                             { key: "company", label: "Company" },
                             { key: "Title", label: "Title" },
                             { key: "start_date", label: "Start Date" },
                             { key: "end_date", label: "End Date" },
                             { key: "is_current", label: "Is current" },
                             { key: "duration_in_months", label: "Duration In Months" }
                           ].map(({ key, label }) => (
                             <TableCell
                               key={key}
                               isHeader
                               className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
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
            {experienceData.map((item,) => (
                <TableRow >
                  <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                    {item.company}
                  </TableCell>
                  <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                    {item.title}
                  </TableCell>
                  <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                    {item.start_date}
                  </TableCell>
                  <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                    {item.end_date}
                  </TableCell>
                  <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                    {item.is_current}
                  </TableCell>
                  <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                    {item.duration_in_months}
                  </TableCell>
                  </TableRow>
              ))}
          </TableBody>
        </Table>
        
      </div>
      </div>
