import React, { useEffect, useState } from 'react';
import axios from 'axios';
import { Bar } from 'react-chartjs-2';

const RefugeeStatistics = () => {
  const [data, setData] = useState({});

  useEffect(() => {
    axios.get('/api/refugee-stats')
      .then(response => setData(response.data))
      .catch(error => console.error('Error fetching data', error));
  }, []);

  const chartData = {
    labels: data.countries,
    datasets: [{
      label: 'Refugees',
      data: data.counts,
      backgroundColor: 'rgba(75, 192, 192, 0.6)',
    }]
  };

  return (
    <div>
      <h2>Refugee Statistics</h2>
      <Bar data={chartData} />
    </div>
  );
};

export default RefugeeStatistics;
