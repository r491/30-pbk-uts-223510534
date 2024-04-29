<template>
 <div id="app">
  <div class="container"> 
    <h1>DAILY ACTIVITY</h1> 
    <p class="title">Kegiatan</p> 
    <table>
      <thead>
        <tr>
          <th>Kegiatan</th>
          <th>Status</th>
          <th>Tindakan</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="activity in activities" :key="activity.id" :class="{ completed: activity.selesai }"> 
          <td>
            <span :class="{ 'completed-text': activity.selesai }">{{ activity.name }}</span> 
          </td>
          <td>
            <span>{{ activity.selesai ? 'Telah Selesai' : 'Belum Selesai' }}</span>
            <input type="checkbox" v-model="activity.selesai">
          </td>
          <td>
            <button @click="cancelActivity(activity.id)">Batalkan</button>
          </td>
        </tr>
      </tbody>
    </table>

    
    <form @submit.prevent="addActivity">
      <br>
      <input type="text" v-model="newActivity" placeholder="">
      <br>
      <button type="submit">Tambahkan</button>
    </form>
  </div>
</div>


<script>
  const { ref } = Vue;

  const activities = ref([
    { id: 1, name: 'Baca Al-Quran', selesai: false },
  ]);

  const newActivity = ref('');

  function addActivity() {
    if (newActivity.value.trim() !== '') {
      activities.value.push({ id: Date.now(), name: newActivity.value, selesai: false });
      newActivity.value = '';
    }
  }

  function cancelActivity(id) {
    const index = activities.value.findIndex(activity => activity.id === id);
    if (index !== -1) {
      activities.value.splice(index, 1);
    }
  }

  Vue.createApp({
    setup() {
      return { activities, newActivity, addActivity, cancelActivity };
    }
  }).mount('#app');
</script>
<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-image: url(back1.avif);
  background-repeat: no-repeat;
  background-size: cover;
}

.container {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  background-color: #000000;
  border-radius: 10px;
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.1);
  animation: fadeIn 0.5s ease; 
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

h1 {
  text-align: center;
  color: #a7a7a7;
  margin-bottom: 10px;
}

h2 {
  color: #666;
  margin-bottom: 20px;
}

.title {
  font-weight: bold;
  font-size: 18px;
  color: #007bff;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
td{
  color: whitesmoke;
}
th{
  color: white;
}


th, td {
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.completed-text {
  text-decoration: line-through;
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

input[type="text"] {
  padding: 8px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

button[type="submit"] {
  background-color: #28a745;
}

button[type="submit"]:hover {
  background-color: #218838;
}


</style>

