return (
    <div className="d-flex flex-col">
    <div className="flex flex-wrap">
        {/* Profile Details Card */}
        <div className="card bg-white m-3 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[50%] lg:h-[10%]">
          <h4 className="card-title">Profile Details</h4>
          <div className="grid grid-cols-1 gap-4 lg:grid-cols-2 lg:gap-7 2xl:gap-x-32">
            {Object.entries({
              "First Name": profileDetails.firstName,
              "Last Name": profileDetails.lastName,
              Email: profileDetails.email,
              Phone: profileDetails.phone,
              "Date of Birth": profileDetails.dob,
              "Total Experience in Months": profileDetails.experience,
              "Notice Period": profileDetails.noticePeriod ?? "-",
              "Expected Joining Date": profileDetails.expectedJoiningDate ?? "-",
              "Current Salary": profileDetails.currentSalary,
              "Expected Salary": profileDetails.expectedSalary,
              Gender: profileDetails.gender,
              City: profileDetails.city,
              "CV Summary": profileDetails.cvSummary,
            }).map(([label, value]) => (
              <div key={label}>
                <p className="subheader">{label}</p>
                <p className="content">{value}</p>
              </div>
            ))}
          </div>
        </div>
        {/* Profile Highlights Card */}
        <div className="card bg-white mt-4 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[46%] lg:h-[20%]">
          <h4 className="card-title">Profile Highlights</h4>
          <div className="grid grid-cols-1 gap-4 lg:grid-cols-2 lg:gap-7 2xl:gap-x-32">
            {Object.entries({
              "Current company Tenure months": profileHighlights.tenureMonths,
              "Team management experience months": profileHighlights.teamMgmtExp ?? "-",
              "Awards count": profileHighlights.awardsCount,
              "Longest company duration month": profileHighlights.longestDuration,
              "Companies worked": profileHighlights.companiesWorked,
              Usp: profileHighlights.usp
            }).map(([label, value]) => (
              <div key={label}>
                <p className="subheader">{label}</p>
                <p className="content">{value}</p>
              </div>
            ))}
          </div>
        </div>
    </div>
    <div className="flex flex-between flex-wrap lg:w-[100%]">
     {/* Experience Table */}
      <div className="max-w-full overflow-x-auto custom-scrollbar flex ">
      <div className="card bg-white ml-3 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[100%] lg:h-[20%]">
        <Table>
          <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
            <TableRow>
              {/* Optional empty header cell if needed */}
              <TableCell isHeader className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]" children={undefined} />
              {[
                { key: "company", label: "Company" },
                { key: "Title", label: "Title" },
                { key: "start_date", label: "Start Date" },
                { key: "end_date", label: "End Date" },
                { key: "is_current", label: "Is Current" },
                { key: "duration_in_months", label: "Duration (Months)" },
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
                    <button className="flex flex-col gap-0.5">
                        <svg
                          className={`text-gray-300 dark:text-gray-700  ${
                            sortKey === key && sortOrder === "asc"
                              ? "text-brand-500"
                              : ""
                          }`}
                          width="8"
                          height="5"
                          viewBox="0 0 8 5"
                          fill="none"
                          xmlns="http://www.w3.org/2000/svg"
                        >
                          <path
                            d="M4.40962 0.585167C4.21057 0.300808 3.78943 0.300807 3.59038 0.585166L1.05071 4.21327C0.81874 4.54466 1.05582 5 1.46033 5H6.53967C6.94418 5 7.18126 4.54466 6.94929 4.21327L4.40962 0.585167Z"
                            fill="currentColor"
                          />
                        </svg>
                        <svg
                          className={`text-gray-300 dark:text-gray-700 `}
                          width="8"
                          height="5"
                          viewBox="0 0 8 5"
                          fill="none"
                          xmlns="http://www.w3.org/2000/svg"
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
          <TableBody>
            {experienceData.map((item, index) => (
              <TableRow key={index}>
                <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {index + 1}
                </TableCell>
                <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.company}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.title}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.start_date}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.end_date}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.is_current ? "Yes" : "No"}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.duration_in_months}
                </TableCell>
              </TableRow>
            ))}
          </TableBody>
        </Table>
      </div>
      </div>
      {/* Education Table */}
      <div className="max-w-full overflow-x-auto custom-scrollbar flex ">
      <div className="card bg-white ml-3 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[100%] lg:h-[20%]">
        <Table>
          <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
            <TableRow>
              {/* Optional empty header cell if needed */}
              <TableCell isHeader className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]" children={undefined} />
              {[
                { key: "organization", label: "organization" },
                { key: "start_year", label: "Start Year" },
                { key: "end_year", label: "End Year" }
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
            {education.map((item, index) => (
              <TableRow key={index}>
                <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {index + 1}
                </TableCell>
                <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.organization}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.start_year}
                </TableCell>
                <TableCell className="px-4 py-4 font-normal text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.end_year}
                </TableCell>
              </TableRow>
            ))}
          </TableBody>
        </Table>
      </div>
      </div>
      {/* skills */}
      <div className="max-w-full overflow-x-auto custom-scrollbar flex ">
      <div className="card bg-white ml-3 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[30%] lg:h-[20%]">
        <Table>
          <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
            <TableRow>
              {/* Optional empty header cell if needed */}
              <TableCell isHeader className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]" children={undefined} />
              {[
                { key: "Skills", label: "Skills Names" }
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
            {skills.map((item, index) => (
              <TableRow key={index}>
                <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {index + 1}
                </TableCell>
                <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap">
                  {item.skill_name}
                </TableCell>
              </TableRow>
            ))}
          </TableBody>
        </Table>
      </div>
      </div>
    </div>  
    </div>
  );
