<script setup>
  import Info from './components/Info.vue'
  import Calendar from './components/Calendar.vue'
  import Message from './components/Message.vue'
  import { ref } from 'vue'

  const infoSubmitted = ref(false)
  const dateSubmitted = ref(false)
  const infoConfirmed = ref(false)
  const messageSent = ref(false)

  const infoData = ref({ 
    name: '', 
    email: '',
    phone: ''
  })

  const dateData = ref({ 
    date: ''
  })

  const messageData = ref({ 
    message: ''
  })

  const handleFormSubmitted = (data) => {
    infoData.value = data
    infoSubmitted.value = true
  }

  const handleDateSubmitted = (data) => {
    dateData.value = data
    dateSubmitted.value = true
  }

  const handleConfirm = () => {
    infoConfirmed.value = true
    const el = document.getElementById('confirmBtn')
    if (el) {
      setTimeout(() => {
          el.style.display = 'none'
      }, 200)
    }
    const el2 = document.getElementById('infoSection')
    const el3 = document.getElementById('dateSection')
    if (el2 && el3) {
      setTimeout(() => {
          el2.parentNode.removeChild(el2)
          el3.parentNode.removeChild(el3)
      }, 200)
    }
  }

  const handleMessageSubmitted = (data) => {
    messageData.value = data
    messageSent.value = true
  }

  const handleNoMessage = ref(true)

  const handleBookMeeting = async () => {
    try {
      const requestData = {
        infoData: infoData.value,
        dateData: dateData.value,
        messageData: handleNoMessage.value ? null : messageData.value
      }
      const response = await fetch('/book-meeting', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(requestData)
      })
      if (response.ok) {
        console.log('Meeting booked successfully!')
      } else {
        console.error('Failed to book meeting:', response.statusText)
      }
    } catch (error) {
      console.error('Error occurred while booking meeting:', error)
    }
  }
</script>

<template>
  <Info @formSubmitted="handleFormSubmitted" id="infoSection" />
  <div v-if="infoSubmitted">
    <Calendar @dateSelected="handleDateSubmitted" id="dateSection" />
    <p>Name: {{ infoData.name }}</p>
    <p>Email: {{ infoData.email }}</p>
    <p>Phone: {{ infoData.phone }}</p>
  </div>
  <div v-if="dateSubmitted">
    <p>Date Selected: {{ dateData.value }}</p>
    <button id="confirmBtn" @click="handleConfirm">Confirm Info and Date</button>
  </div>
  <div v-if="infoConfirmed">
    <button id="noMessageBtn" @click="handleNoMessage = !handleNoMessage">
      <span v-if="handleNoMessage">Book without a message</span>
      <span v-else>Send a message</span>
    </button>
    <div v-if="handleNoMessage">
      <Message @messageSubmitted="handleMessageSubmitted" />
      <p v-if="messageSent">Message: {{ messageData.value }}</p>
    </div>
    <div v-else>
      <p>Book Meeting Without Message</p>
    </div>
  </div>
  <div v-if="infoConfirmed">
    <button id="bookBtn" @click="handleBookMeeting">Book Meeting</button>
  </div>
</template>

<style scoped lang="scss">
  div {
    width: 600px;
    max-width: 600px;
    margin: auto;
  }
</style>
