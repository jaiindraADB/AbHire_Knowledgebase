import { useEffect, useState } from "react";
import axios from 'axios';
const API_BASE_URL = 'https://abhirebackend.onrender.com';

export default function ProfileDetailsCard() {
   const [data, setData] = useState([]);
   const [error ,setError] = useState('');

   useEffect(()=> {
    const fetchData = async () => {
      try{
      const API_URl = `${API_BASE_URL}/hiringflow/steps`;
      const response = await axios.get(API_URl);
      setData(response.data) ;
      console.log(response.data)
    } catch (error) {
      console.log(error);
      setError('Failed fetch');
    }
    };
    fetchData();
   }, []);
  
  return (
    <div className="d-flex flex-col">
    <div className="flex flex-wrap">
     {/* Experience Table */}
      <div className="bg-white dark:bg-white/[0.03] mt-6 p-6 rounded-xl shadow-md w-full lg:w-[100%]">
      <h4 className="text-lg font-semibold mb-4">Experience</h4>
      <table>
        <thead>
          <tr>
            <th>1st</th>
            <th>2nd</th>
            <th>3rd</th>
            <th>4th</th>
          </tr>
        </thead>
      <tbody>
       {data.map((step, index) => {
          <tr key={step.id || index}>
            <td>{step.hiringflow_steps_master_id}</td>
            <td>{step.step_name}</td>
            <td>{step.step_code}</td>
            <td>{step.description}</td>
            <td>{step.step_level}</td>
            <td>{step.is_configurable ? 'yes' : 'No'}</td>
          </tr>
        })} 
      </tbody>
      </table>
    </div>
    </div>  
    </div>
  );
}
