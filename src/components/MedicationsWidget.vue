<template>
    <div class="medications-widget">
      <h2>Medications Widget</h2>
      <div v-if="isLoading">
        Loading medications data...
      </div>
      <div v-else>
        <ul v-if="medications.length > 0">
          <li v-for="medication in medications" :key="medication.id">
            {{ medication.name }} - {{ medication.dosage }}
            <button @click="editMedication(medication)">Edit</button>
            <button @click="deleteMedication(medication)">Delete</button>
          </li>
        </ul>
        <p v-else>No medications found.</p>
      </div>
  
      <div v-if="isEditing" class="edit-medication">
        <input type="text" v-model="editedMedication.name" placeholder="Nama Obat" />
        <input type="text" v-model="editedMedication.dosage" placeholder="Dosis" />
        <button @click="updateMedication">Update</button>
      </div>
  
      <div class="add-medication">
        <input type="text" v-model="newMedicationName" placeholder="Nama Obat" />
        <input type="text" v-model="newMedicationDosage" placeholder="Dosis" />
        <button @click="addMedication">Add Medication</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MedicationsWidget',
    data() {
      return {
        isLoading: true,
        medications: [],
        newMedicationName: '',
        newMedicationDosage: '',
        isEditing: false,
        editedMedication: {}
      };
    },
    mounted() {
      // Simulating an API call to fetch medications data
      setTimeout(() => {
        this.isLoading = false;
        this.medications = [
          { id: 1, name: 'Paracetamol', dosage: '1 tablet' },
          { id: 2, name: 'Tiroid    ', dosage: '1 pills' },
          { id: 3, name: 'Paramex', dosage: '1 tablet' }
        ];
      }, 2000);
    },
    methods: {
      addMedication() {
        if (this.newMedicationName && this.newMedicationDosage) {
          const newMedication = {
            id: this.medications.length + 1,
            name: this.newMedicationName,
            dosage: this.newMedicationDosage
          };
          this.medications.push(newMedication);
          this.newMedicationName = '';
          this.newMedicationDosage = '';
        }
      },
      editMedication(medication) {
        this.isEditing = true;
        this.editedMedication = { ...medication };
      },
      updateMedication() {
        const index = this.medications.findIndex(medication => medication.id === this.editedMedication.id);
        if (index !== -1) {
          this.medications.splice(index, 1, this.editedMedication);
          this.isEditing = false;
          this.editedMedication = {};
        }
      },
      deleteMedication(medication) {
        const index = this.medications.findIndex(item => item.id === medication.id);
        if (index !== -1) {
          this.medications.splice(index, 1);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .medications-widget {
    border: 1px solid #aedddd;
    padding: 20px;
    margin-bottom: 20px;
  }
  
  .medications-widget h2 {
    margin-bottom: 10px;
  }
  
  .medications-widget ul {
    list-style: none;
    padding: 0;
    margin-bottom: 10px;
  }
  
  .medications-widget li {
    margin-bottom: 5px;
  }
  
  .edit-medication input {
    margin-right: 10px;
    padding: 5px;
    border: 1px solid #b7f9fc;
  }
  
  .edit-medication button {
    padding: 5px 10px;
    background-color: #1c2222;
    border: none;
    cursor: pointer;
  }
  
  .edit-medication button:hover {
    background-color: #1c2222;
  }
  
  .add-medication input {
    margin-right: 10px;
    padding: 5px;
    border: 1px solid #b7f9fc;
  }
  
  .add-medication button {
    padding: 5px 10px;
    background-color: #1c2222;
    border: none;
    cursor: pointer;
  }
  
  .add-medication button:hover {
    background-color: #1c2222;
  }
  
  </style>
  