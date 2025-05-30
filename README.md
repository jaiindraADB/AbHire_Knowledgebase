<div className="d-flex flex-col">
    <div className="flex flex-between flex-wrap lg:w-[90%]">
      {/* Education Table */}
     <div className="bg-white dark:bg-white/[0.03] mt-6 p-4 rounded-xl shadow-md w-full lg:w-[110%]">
      <h4 className="text-lg font-semibold mb-4">Canditates</h4>
       <Table>
          <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
            <TableRow>
              {/* Optional empty header cell if needed */}
              <TableCell isHeader className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]" children={undefined} />
              {[
                { key: "full_name", label: "Full Name" },
                { key: "total_experience_in_years", label: "Total Experience in Years" },
                { key: "current_designation", label: "Current Designation" },
                { key: "current_company", label: "Current Company" },
                { key: "jd_matching_score", label: "Jd Matching Score" },
                { key: "notice_period_days", label: "Notice Period Days" },
                { key: "current_salary", label: "Current Salary" },
                { key: "email1", label: "Email" },
                { key: "phone1", label: "Phone" },
                { key: "cv_status_name", label: "Cv Status" },
                { key: "interview_stage", label: "Interview Stage" },
                { key: "uploaded_at", label: "Uploaded At" }
              ].map(({ key, label }) => (
                <TableCell
                  key={key}
                  isHeader
                  className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
                >
                  <div className="flex items-center justify-between cursor-pointer"
                  onClick={() => handleSort(key as SortKey)}>
                    <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                      {label}
                    </p>
                  </div>
                </TableCell>
              ))}
            </TableRow>
          </TableHeader>
          <TableBody>
            {experienceData.map((item, index) => (
              <TableRow key={index}>
                <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {index + 1}
                </TableCell>
                <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-wrap">
                  {item.full_name}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.total_experience_in_years}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.current_designation}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-wrap">
                  {item.current_company}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.jd_matching_score}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.notice_period_days}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.current_salary}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.email1}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.phone1}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.cv_status_name}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.interview_stage}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.tier}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-wrap">
                  {item.uploaded_at}
                </TableCell>
              </TableRow>
            ))}
          </TableBody>
        </Table>
      </div>
      </div>
    </div>  
