<template>
  <div style="border-bottom: 1px solid #ccc; padding: 10px 0;">
    <p>
      <b>{{ friend.fullName }}</b> ({{ friend.birthYear }} р.н.) <br>
      Тел: {{ friend.mobile }} / {{ friend.landline }}
    </p>
    <button @click="$emit('remove', friend.id)">Вилучити</button>
  </div>
</template>

<script>
export default {
  props: ['friend']
}
</script>