<table>
        <thead className="border-t border-gray-100 dark:border-white/[0.05]">
          <tr>
            <td children={undefined} />
            {[
              { key: "company", label: "company" },
              { key: "title", label: "title" },
              { key: "start_date", label: "start_date" },
              { key: "end_date", label: "end_date" },
              { key: "is_current", label: "is_current" },
              { key: "duration_in_months", label: "duration_in_months" },
              { key: "profile_id", label: "profile_id" }
            ].map(({ key, label }) => (
              <td
                key={key}
                className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
              >
                <div
                  className="flex items-center justify-between cursor-pointer"
                >
                  <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                    {label}
                  </p>
                </div>
              </td>
            ))}
            <td
              className="px-4 py-3 border border-gray-100 dark:border-white/[0.05]"
            >
              <p className="font-medium text-gray-700 text-theme-xs dark:text-gray-400">
                Action
              </p>
            </td>
          </tr>
        </thead>
      </table>
