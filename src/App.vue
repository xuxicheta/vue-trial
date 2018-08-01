<template>
  <div id="app">
    <the-event-form class="event-form" />
  </div>
</template>

<script>
import EventForm from './components/EventForm';

export default {
  name: 'App',
  components: {
    'the-event-form': EventForm,
  },
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 14px;
}

.event-form {
  max-width: 600px;
  margin: auto;
}
</style>
