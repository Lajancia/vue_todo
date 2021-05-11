<template>
  <div>
    {{ message }}<br />

    <span :title="message">
      내 위에 잠시 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다!
    </span>
    <p v-if="seen">이제 나를 볼 수 있어요</p>
    <p v-else>나는 쟤랑 반대에요</p>
    <button @click="changeseen">change</button>
    <ol>
      <li v-for="todo in todos" :key="todo.index">
        {{ todo.text }}
      </li>
    </ol>
    <input v-model="message" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "안녕하세요 Vue!",
      seen: true,
      todos: [
        { text: "JavaScript 배우기" },
        { text: "Vue 배우기" },
        { text: "무언가 멋진 것을 만들기" },
      ],
    };
  },
  methods: {
    changeseen() {
      this.seen = !this.seen;
      this.message = "바뀌었다.";
    },
  },
};
</script>

<style lang="scss" scoped></style>
