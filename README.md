
import  { useEffect, useState } from 'react';
import axios from 'axios';
import {
  Table,
  TableBody,
  TableCell,
  TableHeader,
  TableRow
} from "../../components/ui/table";

export default function Practice() {
  const [data, setData] = useState([]);
  const [error, setError] = useState('');

  useEffect(() => {
    const fetchData = async () => {
      try {
        const API_URL = `https://abhirebackend.onrender.com/hiringflow/steps`;
        const response = await axios.get(API_URL);
        setData(Array.isArray(response.data) ? response.data : [response.data]);
      } catch (err) {
        console.error('Fetch error:', err);
        setError('Failed to fetch data.');
      }
    };

    fetchData();
  }, []);

  if (error) return <div className='text-red-600'>{error}</div>;
  if (data.length === 0) return <div>Loading...</div>;

  return (
    <div className="overflow-hidden rounded-2xl bg-white dark:bg-white/[0.03] border border-gray-200 dark:border-gray-800">
      <Table>
        <TableHeader className="border-t border-gray-100 dark:border-white/[0.05]">
          <TableRow>
            <TableCell>Id</TableCell>
            <TableCell>Step Name</TableCell>
            <TableCell>Code</TableCell>
            <TableCell>Description</TableCell>
            <TableCell>Level</TableCell>
            <TableCell>Configurable</TableCell>
            <TableCell>Active</TableCell>
            <TableCell>Created At</TableCell>
          </TableRow>
        </TableHeader>
        <TableBody>
          {data.map((step) => (
            <TableRow key={step.hiringflow_steps_master_id}>
              <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">{step.hiringflow_steps_master_id}</TableCell>
              <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">{step.step_name}</TableCell>
              <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">{step.step_code}</TableCell>
              <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">{step.description}</TableCell>
              <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">{step.step_level}</TableCell>
              <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">{step.is_configurable ? 'Yes' : 'No'}</TableCell>
              <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">{step.is_active ? 'Yes' : 'No'}</TableCell>
              <TableCell className="px-4 py-4 font-medium text-gray-800 border border-gray-100 dark:border-white/[0.05] text-theme-sm dark:text-gray-400 whitespace-nowrap ">{new Date(step.created_at).toLocaleString()}</TableCell>
            </TableRow>
          ))}
        </TableBody>
      </Table>
    </div>
  );
}
