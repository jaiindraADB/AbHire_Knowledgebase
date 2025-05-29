<div className="overflow-x-auto w-full flex mt-4 justify-center">
      <h1>Experience</h1>
  <table className="card bg-white m-3 dark:bg-white/[0.03] p-6 rounded-xl shadow-md w-full lg:w-[35%]">
    <thead className="bg-gray-50 dark:bg-white/[0.03]">
      <tr>
        <th className="border border-gray-200 dark:border-white/[0.05] px-4 py-2" />
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
      </tr>
    </thead>
    {/* You can add tbody rows here */}
  </table>
</div>
