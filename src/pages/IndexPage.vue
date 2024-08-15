<template>
  <q-page class="flex flex-center">
    <div class="chat" style="max-width: 800px; width: 100%">
      <div>
        <q-scroll-area style="height: 85vh">
          <q-chat-message
            v-for="(questions, index) in dataQuestions"
            :key="index"
            name="LLaMa"
            avatar="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQfCa7754iGW449xF4tVvkbu3YzKQmo068a7w&s"
            :text="[questions.question]"
            sent
          />
          <q-chat-message
            name="Senior Aman"
            avatar="https://cdn.quasar.dev/img/avatar2.jpg"
            :text="['doing fine, how r you?']"
          />
        </q-scroll-area>
      </div>
    </div>
    <div class="container-form">
      <q-btn
        class="upload-file"
        flat
        icon="attach_file"
        size="15px"
        @click="openFileDialog"
        :color="isDarkMode ? 'white' : 'black'"
      />
      <q-input
        class="qinput"
        v-model="fileName"
        placeholder="Сообщить LLaMa"
        type="text"
        borderless
        :style="inputStyle"
      />
      <q-btn
        outlined
        size="20px"
        class="send-data"
        flat
        icon="arrow_circle_up"
        @click="sendData"
        :color="isDarkMode ? 'white' : 'black'"
        :style="buttonStyle"
        rounded
      />
    </div>
    <input
      type="file"
      ref="fileInput"
      @change="handleFileChange"
      style="display: none"
    />
  </q-page>
</template>

<script setup>
import { Dark } from "quasar";
import { ref, computed } from "vue";

const isDarkMode = ref(Dark.isActive);

const fileName = ref("");
const fileInput = ref(null);
const dataQuestions = ref([
  {
    id: 1,
    question: "Hi my name is Aman",
  },
  {
    id: 2,
    question: "I am the best person in the GTS",
  },
]);

const sendData = () => {
  if (fileName.value.trim()) {
    const newQuestion = {
      id: dataQuestions.value.length + 1,
      question: fileName.value.trim(),
    };

    dataQuestions.value.push(newQuestion);
    fileName.value = "";
  }
};

const openFileDialog = () => {
  fileInput.value.click();
};

const handleFileChange = (event) => {
  const file = event.target.files[0];
  if (file) {
    fileName.value = file.name;
  }
};

const inputStyle = computed(() => ({
  "--q-placeholder-color": isDarkMode.value ? "white" : "black",
  color: isDarkMode.value ? "white" : "black",
  backgroundColor: isDarkMode.value ? "#333333" : "#eeeeee",
}));

const buttonStyle = computed(() => ({
  backgroundColor: isDarkMode.value ? "#444444" : "#e9ecef",
  color: isDarkMode.value ? "white" : "grey",
}));
</script>

<style scoped>
.q-page {
  display: flex;
  flex-direction: column;
  padding: 0;
  margin: 0;
}

.chat {
  flex: 1;
}

.container-form {
  position: relative;
  display: flex;
  align-items: center;
}

.qinput {
  width: 800px;
  height: 60px;
  border-radius: 30px;
  border: none;
  padding: 0 50px;
  font-size: 17px;
}

.upload-file {
  position: absolute;
  left: 2px;
}

.send-data {
  position: absolute;
  right: 2px;
}

@media (max-width: 810px) {
  .qinput {
    width: 400px;
    padding: 0 50px;
  }
}
</style>
