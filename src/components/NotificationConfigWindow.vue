<template>
  <div>
    <h5>Напоминания</h5>
    <el-row v-for="reminder in notifications" :key="reminder.id" class="row">
      <el-col :span="11" >
        <el-select v-model="reminder.time" placeholder="Select">
          <el-option label="0 минут" value="0"/>
          <el-option label="5 минут" value="5"/>
          <el-option label="10 минут" value="10"/>
        </el-select>
      </el-col>
       <el-col :span="2">&nbsp;</el-col>
      <el-col :span="11">
        <div>
          <el-radio v-model="reminder.type" label="notify">Оповещение</el-radio>
        </div>
        <div>
          <el-radio v-model="reminder.type" label="email">Электронная почта</el-radio>
        </div>
      </el-col>
    </el-row>
    <el-row class="button-row row">
      <el-tooltip effect="dark" content="Добавить напоминание" placement="top-start">
        <button class="button-add" @click="addReminder">+</button>
      </el-tooltip>
    </el-row>
    <el-row class="button-row">
      <el-button @click="$emit('canceled')">Отмена</el-button>
      <el-button type="primary" @click="$emit('updated', config)">Сохранить</el-button>
    </el-row>
  </div>
</template>

<script>
export default {
  props: [
    'visible',
    'notificationConfig',
  ],
  data() {
    return {
      notifications: [],
    };
  },
  created() {
    this.notifications = this.notificationConfig.slice();
  },
  methods: {
    addReminder() {
      this.notifications.push({
        id: this.notifications.length,
        time: 0,
        type: 'nofity',
      });
    },
  },
};
</script>

<style>
  .row {
    margin-bottom: 10px;
  }
  .button-row {
    text-align: right;
    margin-right: 20px;
  }

  .button-add {
    background: #3a8ee6;
    border-radius: 30px;
    border: none;
    color: white;
    cursor: pointer;
    display: inline-block;
    height: 30px;
    line-height: 30px;
    text-align: center;
    width: 30px;
  }
</style>

