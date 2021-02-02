<template>
  <div>
    <div class="full-width">
      <h1>Home</h1>
      <h2 v-if="participants.length !== 0">Welkom {{participants[participants.length - 1].naam}} bij de cursus.</h2>
      <div class="participants-list">
        <ListItem 
          v-for="(participant, index) in participants" 
          :key="index"
          :isEditable="participant.editable"
          :name="participant.naam"
          :team="participant.afdeling"
          :index="index"
          :onDeleteClick="deleteItem"
          @toggle-editable="toggleEditable"
          @click-delete="deleteItem"
        />
      </div>
      <form>
        <h2>Voeg een deelnemer toe:</h2>
        <input type="text" v-model="form.naam" placeholder="Naam">
        <input type="text" v-model="form.afdeling" placeholder="afdeling">
        <button @click="onSubmit">Toevoegen</button>
      </form>
    </div>
  </div>
</template>

<style lang="scss">
  form {
    input[type=text] {
      margin-bottom: 8px;
    }
  }

  .button-container {
    display: none;
    align-items: center;

    .button {
      display: block;
      margin-left: 8px;
      cursor: pointer;

      &.circular {
        width: 24px;
        height: 24px;

        border-radius: 100%;
      }

      &.delete {
        background-color: #e74c3c;
        background-image: url('~@/assets/images/icons/cancel.svg');
        background-position: center;
        background-repeat: no-repeat;
      }

      &.edit {
        border: 1px solid grey;
        background-size: 16px;
        background-image: url('~@/assets/images/icons/edit.svg');
        background-position: center;
        background-repeat: no-repeat;

        &.confirm {
          border: none;
          background-size: 18px;
          background-image: url('~@/assets/images/icons/check.svg');
          background-color: #2ecc71;
        }
      }
    }

  }

</style>

<script>
import ListItem from '@/components/ListItem.vue';
export default {
  name: 'Home',
  components: {
    ListItem
  },
  data() {
    return {
      form: {
        naam: '',
        afdeling: ''
      },
      participants: []
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if(!this.form.naam || !this.form.afdeling) {
        return false;
      }

      this.axios.post('http://dump.lwdev.nl/vue-cursus-api/addDeelnemer/', {
        naam: this.form.naam,
        afdeling: this.form.afdeling
      }).then(() => this.getParticipants());

      this.form.naam = '';
      this.form.afdeling = '';
    },
    deleteItem(index) {
      this.axios.post("http://dump.lwdev.nl/vue-cursus-api/deleteDeelnemer/", {
        id: this.participants[index].id
      }).then(() => this.getParticipants());
    },
    toggleEditable(index) {
      this.participants[index].editable = !this.participants[index].editable;
    },
    getParticipants() {
      this.axios.get('http://dump.lwdev.nl/vue-cursus-api/deelnemers/').then((response) => {
        this.participants = response.data.map(deelnemer => {
          return {
            ...deelnemer,
            editable: false
          }
        });
      })
    }
  },
  created() {
    this.getParticipants();
  }
}
</script>
