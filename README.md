<div className="overflow-hidden rounded-2xl bg-white dark:bg-white/[0.03] border border-gray-200 dark:border-gray-800 ml-[-6vw] lg:w-[119%]">
        <div className="flex flex-col gap-2 px-4 py-4 border border-b-0 border-gray-100 dark:border-white/[0.05] rounded-t-xl sm:flex-row sm:items-center sm:justify-between">
          <div>
            <h3 className="text-base font-medium text-gray-800 dark:text-white/90">
              Select Job Post
            </h3>
          </div>
        </div>
        <div className="max-w-full overflow-x-auto custom-scrollbar m-[20px]">
          <div>
            <Table>
              <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
                <TableRow>
                  <TableCell children={undefined} />
                  {[
                    { key: "Job Code", label: "Job Code" },
                    { key: "total_experience_in_years", label: "Title" },
                    { key: "current_designation", label: "Location" },
                    { key: "current_company", label: "Department" },
                    { key: "jd_matching_score", label: "Client" },
                    { key: "notice_period_days", label: "Open Positions" },
                    { key: "current_salary", label: "Experience" },
                    { key: "expected_salary", label: "Salary" },
                    { key: "location", label: "Status" },
                    { key: "cv_status_name", label: "Recruiter" },
                    { key: "ai_tip", label: "Notes" }
                  ].map(({ key, label }) => (
                    <TableCell
                      key={key}
                      isHeader
                      className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
                    >
                      <div
                        className="flex items-center justify-between cursor-pointer"
                        onClick={() => handleSort(key as SortKey)}
                      >
                        <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                          {label}
                        </p>
                        <button className="flex flex-col gap-0.5">
                          <svg
                            className={`text-gray-300 dark:text-gray-700  ${sortKey === key && sortOrder === "asc"
                                ? "text-brand-500"
                                : ""}`}
                            width="8"
                            height="5"
                            viewBox="0 0 8 5"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                          >
                            <path
                              d="M4.40962 0.585167C4.21057 0.300808 3.78943 0.300807 3.59038 0.585166L1.05071 4.21327C0.81874 4.54466 1.05582 5 1.46033 5H6.53967C6.94418 5 7.18126 4.54466 6.94929 4.21327L4.40962 0.585167Z"
                              fill="currentColor" />
                          </svg>
                          <svg
                            className={`text-gray-300 dark:text-gray-700  ${sortKey === key && sortOrder === "desc"
                                ? "text-brand-500"
                                : ""}`}
                            width="8"
                            height="5"
                            viewBox="0 0 8 5"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                          >
                            <path
                              d="M4.40962 4.41483C4.21057 4.69919 3.78943 4.69919 3.59038 4.41483L1.05071 0.786732C0.81874 0.455343 1.05582 0 1.46033 0H6.53967C6.94418 0 7.18126 0.455342 6.94929 0.786731L4.40962 4.41483Z"
                              fill="currentColor" />
                          </svg>
                        </button>
                      </div>
                    </TableCell>
                  ))}

                </TableRow>
              </TableHeader>

              <TableBody>
                {currentData.map((item, i) => (
                  <TableRow>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-wrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">
                      {i}
                    </TableCell>
                    <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-white/90 whitespace-nowrap ">
                      <div className="flex justify-center w-full gap-2">
                        <Link
                          to={`/candidateprofile`}
                          className="text-gray-500 hover:text-gray-800 dark:text-gray-400 dark:hover:text-white/90"
                        >
                          <PencilIcon className="size-5" />
                        </Link>

                        {/* Add Schedule Interview link/button */}
                        {jobId && (
                          <Link
                            to={`/schedule-interview/${jobId}/${item.profile_id || i + 1}`}
                            className="flex items-center gap-1 px-2 py-1 text-xs font-medium rounded-md bg-brand-50 text-brand-600 hover:bg-brand-100 dark:bg-brand-900/30 dark:text-brand-400 dark:hover:bg-brand-900/50"
                            title="Schedule Interview"
                          >
                            <svg className="size-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                            </svg>
                            Schedule
                          </Link>
                        )}
                      </div>
                    </TableCell>
                  </TableRow>
                ))}
              </TableBody>
            </Table>
          </div>
        </div>
      </div>
