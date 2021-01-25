<template>
  <div>
    <div class="full-width">
      <h1>Home</h1>
      <h2 v-if="participants.length !== 0">Welkom {{participants[participants.length - 1].name}} bij de cursus.</h2>
      <div class="participants-list">
        <div v-for="(participant, index) in participants" :key="index" class="list-item">
          <div class="body" v-if="!participant.editable">
            <h3>{{participant.name}}</h3>
            <p>{{participant.team}}</p>
          </div>
          <div class="body" v-else>
            <input type="text" v-model="participant.name">
            <input type="text" v-model="participant.team">
          </div>
          <div class="button-container">
            <div @click="toggleEditable(index)" class="button edit circular" :class="{ confirm: participant.editable }"></div>
            <div @click="deleteItem(index)" class="button delete circular"></div>
          </div>
        </div>
      </div>
      <form>
        <h2>Voeg een deelnemer toe:</h2>
        <input type="text" v-model="form.name" placeholder="Naam">
        <input type="text" v-model="form.team" name="team" placeholder="Team">
        <button @click="onSubmit">Toevoegen</button>
      </form>
    </div>
  </div>
</template>

<style lang="scss">
  .list-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    padding: 12px 0;
    border-bottom: 1px solid grey;

    &:hover {
      .button-container {
        display: flex;
      }
    }
  }

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
export default {
  name: 'Home',
  data() {
    return {
      form: {
        name: '',
        team: ''
      },
      participants: [
        {
          name: 'Dennis',
          team: 'engagement',
          editable: false
        }, {
          name: 'Jeffrey',
          team: 'engagement',
          editable: false
        }, {
          name: 'Pim',
          team: 'platforms',
          editable: false
        }, {
          name: 'Tom',
          team: 'platforms',
          editable: false
        }
      ]
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if(!this.form.name || !this.form.team) {
        return false;
      }

      this.participants.push({
        name: this.form.name,
        team: this.form.team,
        editable: false
      });

      this.form.name = '';
      this.form.team = '';
    },
    deleteItem(index) {
      this.participants.splice(index, 1);
    },
    toggleEditable(index) {
      this.participants[index].editable = !this.participants[index].editable;
    }
  }
}
</script>
