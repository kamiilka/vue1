<template>
  <div>
    <h3>Телефонний довідник</h3>
    
    <label>Пошук: </label>
    <input 
      type="text" 
      v-model="searchQuery" 
      placeholder="Введіть ПІБ, рік або номер..." 
    />
    <br><br>

    <div v-if="filteredFriends.length > 0">
      <FriendItem 
        v-for="item in filteredFriends" 
        :key="item.id" 
        :friend="item" 
        @remove="deleteFriend"
      />
    </div>
    <p v-else>За вашим запитом нічого не знайдено</p>
  </div>
</template>

<script>
import FriendItem from './FriendItem.vue';

export default {
  components: { FriendItem },
  data() {
    return {
      searchQuery: '',
      friends: [
        { id: 1, fullName: 'Іванов Іван Іванович', birthYear: 1995, landline: '031224455', mobile: '0501112233' },
        { id: 2, fullName: 'Петров Петро Петрович', birthYear: 1988, landline: '031226677', mobile: '0664445566' },
        { id: 3, fullName: 'Сидоров Олег Олегович', birthYear: 2000, landline: '031228899', mobile: '0937778899' }
      ]
    };
  },
  computed: {

    filteredFriends() {
      const query = this.searchQuery.toLowerCase();
      
      return this.friends.filter(f => {

        return (
          f.fullName.toLowerCase().includes(query) ||
          f.birthYear.toString().includes(query) ||
          f.landline.includes(query) ||
          f.mobile.includes(query)
        );
      });
    }
  },
  methods: {
    deleteFriend(id) {
      this.friends = this.friends.filter(f => f.id !== id);
    }
  }
}
</script>