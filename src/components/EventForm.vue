<template>
  <div>
    <el-form
      ref="form"
      :model="form"
      :rules="rules"
      label-width="200px"
    >

      <el-form-item label="Название события" prop="name">
        <el-input v-model="form.name"></el-input>
      </el-form-item>

      <el-form-item label="Дата - время" required="">
        <el-col :span="11">
          <el-form-item prop="date">
            <el-date-picker type="date" placeholder="Выберите дату" v-model="form.date" style="width: 100%;"></el-date-picker>
          </el-form-item>
        </el-col>

        <el-col class="line" :span="2" style="text-align: center">-</el-col>

        <el-col :span="11">
          <el-form-item prop="time">
            <el-time-picker type="fixed-time" placeholder="Выберите время" v-model="form.time" style="width: 100%;"></el-time-picker>
          </el-form-item>
        </el-col>
      </el-form-item>

      <el-form-item label="Уведомления">
        <el-button icon="el-icon-setting" @click="onNotificationConfigOpen">Настройка уведомлений</el-button>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="onSubmit">Создать</el-button>
        <el-button @click="onCancel">Отмена</el-button>
      </el-form-item>

    </el-form>


    <el-dialog
      title="Настройки уведомлений"
      :visible.sync="dialogVisible"
      width="40%"
    >
      <the-notification-config-window
        :notificationConfig="notificationConfig"
        :visible.sync="dialogVisible"
        @updated="onNotificationUpdated($event)"
        @canceled="onNotificationCanceled"
      />
    </el-dialog>
  </div>
</template>
<script>
import NotificationConfigWindow from './NotificationConfigWindow';

export default {
  components: {
    'the-notification-config-window': NotificationConfigWindow,
  },
  data() {
    return {
      form: {
        name: '',
        time: '',
        date: '',
      },
      rules: {
        name: [
          { required: true, message: 'Введите название', trigger: 'blur' },
          { min: 3, max: 50, message: 'Длина должна быть от 3 до 50 символов', trigger: 'blur' },
        ],
        date: [
          { type: 'date', required: true, message: 'Выберите дату', trigger: 'change' },
        ],
        time: [
          { type: 'date', required: true, message: 'Выберите время', trigger: 'change' },
        ],
      },
      notificationConfig: [
        {
          id: 0,
          time: 0,
          type: 'notify',
        },
      ],
      dialogVisible: false,
    };
  },
  methods: {
    onSubmit() {
      this.$refs.form.validate((valid) => {
        if (valid) {
          /* eslint-disable */
          console.log('Название: ', this.name);
          console.log('Дата', this.date.toLocaleString());
          console.log('Время', this.time.toLocaleString());
          this.notificationConfig.forEach((reminder) => {
            console.log('- Уведомление - ');
            console.log('Время', reminder.time);
            console.log('Тип', reminder.type);
          });
          this.$refs.form.resetFields();
          return true;
        }
        return false;
      });
    },
    onCancel() {
      this.$refs.form.resetFields();
    },
    onNotificationConfigOpen() {
      this.dialogVisible = true;
    },
    onNotificationUpdated(event) {
      this.notificationConfig = event.slice();
      this.dialogVisible = false;
    },
    onNotificationCanceled() {
      this.dialogVisible = false;
    },
  },
};
</script>

