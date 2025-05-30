<div className="d-flex flex-column">
    <div>
      <div className="flex justify-center">
      <div className="card bg-white m-3 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[35%]">
        <div className="flex flex-col gap-6 lg:flex-row lg:items-start lg:justify-between">
          <div>
            <h4 className="card-title">Profile Details</h4>
            <div className="grid grid-cols-1 gap-4 lg:grid-cols-2 lg:gap-7 2xl:gap-x-32">
              <div>
                <p className="subheader">First Name</p>
                <p className="content">Harmeet</p>
              </div>
              <div>
                <p className="subheader">Last Name</p>
                <p className="content">Arora</p>
              </div>
              <div>
                <p className="subheader">Email</p>
                <p className="content">harmeeta2@gmail.com</p>
              </div>
              <div>
                <p className="subheader">Phone</p>
                <p className="content">7972195259</p>
              </div>
              <div>
                <p className="subheader">Date of Birth</p>
                <p className="content">2025-08-02</p>
              </div>
              <div>
                <p className="subheader">Total Experience in Months</p>
                <p className="content">111</p>
              </div>
              <div>
                <p className="subheader">Notice Period</p>
                <p className="content">null</p>
              </div>
              <div>
                <p className="subheader">Expected Joining Date</p>
                <p className="content">null</p>
              </div>
              <div>
                <p className="subheader">CV Summary</p>
                <p className="content">
                  Currently working as a Content Writer with Astral Informatics Limited since Feb 2022.
                  Expertise in management and development of content for various websites. Passionate about
                  learning new techniques and concepts.
                </p>
              </div>
              <div>
                <p className="subheader">Current Salary</p>
                <p className="content">Current salary</p>
              </div>
              <div>
                <p className="subheader">Expected Salary</p>
                <p className="content">Expected salary</p>
              </div>
              <div>
                <p className="subheader">Gender</p>
                <p className="content">Female</p>
              </div>
              <div>
                <p className="subheader">City</p>
                <p className="content">city</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div className="card bg-white m-3 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[38%] lg:h-[20%]">
        <div className="flex flex-col gap-6 lg:flex-row lg:items-start lg:justify-between">
          <div>
            <h4 className="card-title">Profile Highlights</h4>
            <div className="grid grid-cols-1 gap-4 lg:grid-cols-2 lg:gap-7 2xl:gap-x-32">
              <div>
                <p className="subheader">Current company Tenure months</p>
                <p className="content">39</p>
              </div>
              <div>
                <p className="subheader">Team management experience months</p>
                <p className="content">null</p>
              </div>
              <div>
                <p className="subheader">Awards count</p>
                <p className="content">2</p>
              </div>
              <div>
                <p className="subheader">Longest company duration month</p>
                <p className="content">39</p>
              </div>
              <div>
                <p className="subheader">Companies worked</p>
                <p className="content">5</p>
              </div>
              <div>
                <p className="subheader">Usp</p>
                <p className="content">Passionate Content Writer with expertise in managing and developing content for
                  various websites. Skilled in SEO strategies,   keyword research, and creating compelling content across different niches.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    </div>
   <div className="ml-4">
     <div className="overflow-x-auto w-full">
  <table className="table-auto border-collapse border border-gray-200 dark:border-white/[0.1] w-auto">
    <thead className="bg-gray-50 dark:bg-white/[0.03]">
      <tr>
        <th className="border border-gray-200 dark:border-white/[0.05] px-4 py-2">#</th>
        {[
          { key: "company", label: "Company" },
          { key: "title", label: "Title" },
          { key: "start_date", label: "Start Date" },
          { key: "end_date", label: "End Date" },
          { key: "is_current", label: "Is Current" },
          { key: "duration_in_months", label: "Duration (Months)" },
          { key: "profile_id", label: "Profile ID" }
        ].map(({ key, label }) => (
          <th
            key={key}
            className="px-4 py-2 border border-gray-200 dark:border-white/[0.05] text-sm text-gray-700 dark:text-gray-400 font-semibold text-left"
          >
            {label}
          </th>
        ))}
        <th className="px-4 py-2 border border-gray-200 dark:border-white/[0.05] text-sm text-gray-700 dark:text-gray-400 font-semibold text-left">
          Action
        </th>
      </tr>
    </thead>
    <tbody>
      {[
        {
          company: "Astral Informatics Limited",
          title: "Content Writer",
          start_date: "2022-02-01",
          end_date: "2025-05-28",
          is_current: "true",
          duration_in_months: 39,
          profile_id: 40,
        },
        {
            company: "Japji Travels",
            title: "Freelancer",
            start_date: "2022-01-01",
            end_date: "2023-01-01",
            is_current: "false",
            duration_in_months: 12,
            profile_id: 40,
        },
        {
          company: "Talentica Software Ltd",
          title: "",
          start_date: "2012-11-01",
        end_date: "2016-01-01",
        is_current: "false",
        duration_in_month: 38,
        profile_id: 40,
        },
        {
          company: "Aricent Group",
          title: "",
          start_date: "2011-07-01",
          end_date: "2012-07-01",
          is_current: "false",
          duration_in_months: 12,
          profile_id: 40,
        },
        {
          company: "Videocon Industries (Mobiles)",
          title: "",
          start_date: "2010-08-01",
          end_date: "2011-06-01",
          is_current: "false",
          duration_in_months: 10,
          profile_id: 40,
        }
      ].map((row, index) => (
        <tr key={index} className="bg-white dark:bg-gray-900 hover:bg-gray-50 dark:hover:bg-gray-800">
          <td className="border px-4 py-2 text-sm text-gray-800 dark:text-gray-200">{index + 1}</td>
          <td className="border px-4 py-2">{row.company}</td>
          <td className="border px-4 py-2">{row.title}</td>
          <td className="border px-4 py-2">{row.start_date}</td>
          <td className="border px-4 py-2">{row.end_date || "-"}</td>
          <td className="border px-4 py-2">{row.is_current}</td>
          <td className="border px-4 py-2">{row.duration_in_months}</td>
          <td className="border px-4 py-2">{row.profile_id}</td>
          <td className="border px-4 py-2">
            <button className="text-blue-600 hover:underline dark:text-blue-400">Edit</button>
          </td>
        </tr>
      ))}
    </tbody>
  </table>
    </div>
   </div>
    </div>
