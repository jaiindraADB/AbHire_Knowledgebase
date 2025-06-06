import React , { useEffect , useState} from 'react';
import axios from 'axios';
import {
  Table,
  TableBody,
  TableCell,
  TableHeader,
  TableRow
} from "../../components/ui/table";

export default function Practice() {
    const [setData, setDatafun] = useState([]);
    const [error, setError] = useState(' ');
    useEffect(async () => {
        const API_URL = `https://abhirebackend.onrender.com/hiringflow/steps`;
       const response =  await axios.get(API_URL)
        console.log(response.data);
        
        
    }, []);
    if (error) return <div className='tetx-red-600'>{error}</div>;
    if (SVGTextPositioningElement.length === 0) return <div>Loading...</div>

    return (
        <div className="overflow-hidden rounded-2xl bg-white dark:bg-white/[0.03] border border-gray-200 dark:border-gray-800 ml-[-6vw] lg:w-[119%]">
            <Table>
                <TableHeader>
                    <TableRow>
                        <TableCell>
                        id
                        </TableCell>
                        <TableCell>
                        step name
                        </TableCell>
                        <TableCell>
                        code
                        </TableCell>
                        <TableCell>
                        Description
                        </TableCell>
                        <TableCell>
                        level
                        </TableCell>
                        <TableCell>
                        configurable
                        </TableCell>
                        <TableCell>
                        Active
                        </TableCell>
                        <TableCell>
                        created at
                        </TableCell>
                    </TableRow>
                </TableHeader>
                <TableBody>
                    {setData.map((set: { hiringflow_steps_master_id: string | number | bigint | boolean | React.ReactElement<unknown, string | React.JSXElementConstructor<any>> | Iterable<React.ReactNode> | React.ReactPortal | Promise<string | number | bigint | boolean | React.ReactPortal | React.ReactElement<unknown, string | React.JSXElementConstructor<any>> | Iterable<React.ReactNode> | null | undefined> | null | undefined; }) => (
                        <TableRow>
                        <TableCell>
                            {set.hiringflow_steps_master_id}
                        </TableCell>
                    </TableRow>
                    ))}
                </TableBody>
            </Table>
        </div>
    )
}

function then(arg0: (response: any) => void) {
    throw new Error('Function not implemented.');
}

