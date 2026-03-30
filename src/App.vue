<template>
  <div>
    <h1>Телефонний довідник</h1>

    <div>
      <label>Категорія (тільки текст): </label>
      <CustomInput v-model.capitalize="category" />
      <span> Поточна категорія: {{ category }}</span>
    </div>

    <hr>

    <FriendsList />
  </div>
</template>

<script>
import FriendsList from './components/FriendsList.vue';
import CustomInput from './components/CustomInput.vue';

export default {
  components: { 
    FriendsList, 
    CustomInput 
  },
  data() {
    return {
      category: 'Друзі'
    };
  }
}
</script>