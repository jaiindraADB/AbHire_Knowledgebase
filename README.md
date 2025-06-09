import { useEffect, useState } from "react";
import axios from 'axios';

const API_BASE_URL = 'https://abhirebackend.onrender.com';

export default function ProfileDetailsCard() {
  const [data, setData] = useState([]);
  const [error, setError] = useState('');

  useEffect(() => {
    const fetchData = async () => {
      try {
        const API_URL = `${API_BASE_URL}/hiringflow/steps`;
        const response = await axios.get(API_URL);
        setData(response.data); // Direct array from API
        console.log(response.data);
      } catch (error) {
        console.error(error);
        setError('Failed to fetch');
      }
    };
    fetchData();
  }, []);

  return (
    <div className="d-flex flex-col">
      <div className="flex flex-wrap">
        <div className="bg-white dark:bg-white/[0.03] mt-6 p-6 rounded-xl shadow-md w-full">
          <h4 className="text-lg font-semibold mb-4">Experience</h4>
          <table className="table-auto w-full border-collapse border border-gray-300">
            <thead className="bg-gray-100">
              <tr>
                <th className="border px-4 py-2">ID</th>
                <th className="border px-4 py-2">Step Name</th>
                <th className="border px-4 py-2">Step Code</th>
                <th className="border px-4 py-2">Description</th>
                <th className="border px-4 py-2">Level</th>
                <th className="border px-4 py-2">Configurable</th>
              </tr>
            </thead>
            <tbody>
              {data.map((step, index) => (
                <tr key={ index}>
                  <td className="border px-4 py-2">{step.hiringflow_steps_master_id}</td>
                  <td className="border px-4 py-2">{step.step_name}</td>
                  <td className="border px-4 py-2">{step.step_code}</td>
                  <td className="border px-4 py-2">{step.description}</td>
                  <td className="border px-4 py-2">{step.step_level}</td>
                  <td className="border px-4 py-2">{step.is_configurable ? 'Yes' : 'No'}</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </div>
    </div>
  );
}
