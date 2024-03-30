<script setup>
  import Info from './components/Info.vue'
  import Calendar from './components/Calendar.vue'
  import Message from './components/Message.vue'
  import { ref } from 'vue'

  const infoEditable = ref(true)
  const datePicker = ref(true)
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
      }, 0)
    }
    infoEditable.value = false
    datePicker.value = false
  }

  const backToInfo = () => {
    infoConfirmed.value = false
    const el = document.getElementById('confirmBtn')
    if (el) {
      setTimeout(() => {
          el.style.display = 'block'
      }, 0)
    }
    infoEditable.value = true
    datePicker.value = true
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
  <div id="wrap">
    <Info @formSubmitted="handleFormSubmitted" v-if="infoEditable" />
    <div class="infoDetails" v-if="infoSubmitted">
      <Calendar @dateSelected="handleDateSubmitted" v-if="datePicker" />
      <h2>Info Submitted:</h2>
      <span>Name:</span>
      <p>{{ infoData.name }}</p>
      <span>Email:</span>
      <p>{{ infoData.email }}</p>
      <span>Phone:</span>
      <p>{{ infoData.phone }}</p>
    </div>
    <div class="infoDetails" v-if="dateSubmitted">
      <span>Date Selected:</span>
      <p>{{ dateData.value }}</p>
      <button id="confirmBtn" @click="handleConfirm">Confirm Info and Date</button>
    </div>
    <div id="backBtn" v-if="infoConfirmed">
      <button @click="backToInfo">Back</button>
    </div>
    <div id="messageDetails" v-if="infoConfirmed">
      <button @click="handleNoMessage = !handleNoMessage">
        <span v-if="handleNoMessage">Book without a message</span>
        <span v-else>Send a message</span>
      </button>
      <div v-if="handleNoMessage">
        <Message @messageSubmitted="handleMessageSubmitted" />
        <div v-if="messageSent">
          <span>Message:</span>
          <p>{{ messageData.value }}</p>
        </div>
      </div>
      <div v-else>
        <p>Book Meeting Without Message</p>
      </div>
    </div>
    <div id="bookBtn" v-if="infoConfirmed">
      <button @click="handleBookMeeting">Book Meeting</button>
    </div>
  </div>
</template>

<style scoped lang="scss">
  #wrap {
    width: 600px;
    min-width: 600px;
    margin: 25px auto 0 auto;
    padding: 50px;
    background-color: var(--vt-c-indigo);
    border-radius: 8px;
    @media only screen and (max-width: 600px) {
      width: 95%;
      min-width: 95%;
    }
    .infoDetails {
      text-align: center;
      span {
        font-size: 12px;
        font-weight: bold;
      }
      p {
        line-height: 12px;
        margin-bottom: 15px;
      }
      #confirmBtn{ 
        margin-top: 25px;
        background-color: #04AA6D;
      }
    }
    #backBtn {
      position: absolute;
      top: 10px;
      button {
        background-color: #aa0404;
        padding: 5px 15px;
      }
    }
    #messageDetails {
      text-align: center;
      span {
        font-size: 12px;
        font-weight: bold;
      }
      p {
        line-height: 12px;
        margin-bottom: 15px;
      }
      button {
        background-color: var(--vt-c-text-dark-2);
        padding: 5px 0;
        margin: 10px 0;
        width: 200px;
        font-size: 12px;
      }
    }
    #bookBtn {
      text-align: center;
      margin-top: 50px;
      button {
        background-color: #044caa;
      }
    }
  }
</style>
