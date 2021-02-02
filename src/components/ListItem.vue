<template>
    <div class="list-item">
        <div class="body" v-if="!isEditable">
            <h3>{{name}}</h3>
            <p>{{team}}</p>
        </div>
        <div class="body" v-else>
            <input type="text" v-model="name">
            <input type="text" v-model="team">
        </div>
        <div class="button-container">
            <div @click="onEditClick(index)" class="button edit circular" :class="{ confirm: isEditable }"></div>
            <div @click="onDeleteClick(index)" class="button delete circular"></div>
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
</style>

<script>
export default {
  name: "ListItem",
  props: {
    isEditable: Boolean || null,
    name: String || null,
    team: String || null,
    index: Number || null
  },
  methods: {
    onEditClick(index) {
        this.$emit('toggle-editable', index);
    },
    onDeleteClick(index) {
        this.$emit('click-delete', index);
    }
  }
};
</script>