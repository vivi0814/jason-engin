<template>
  <div class="contact-view">
    <div class="page-header">
      <div class="container">
        <h1>聯絡我們</h1>
        <p>我們期待您的來信。</p>
      </div>
    </div>

    <div class="container content-section">
      <div class="row">
        <div class="col-info">
          <h2>保持聯繫</h2>
          <p class="intro">無論對專案有任何疑問，我們的團隊隨時準備回答您的所有問題。</p>
          
          <div class="contact-details">
            <div class="detail-item">
              <h3>地址</h3>
              <p>新北市板橋區館前西路6號7樓</p>
            </div>
            <div class="detail-item">
              <h3>電話</h3>
              <p>(02)8952-3999</p>
            </div>
            <div class="detail-item">
              <h3>Email</h3>
              <p>jason.apply@msa.hinet.net</p>
            </div>
            <div class="detail-item">
              <h3>營業時間</h3>
              <p>週一至週五: 9:00 AM - 6:00 PM</p>
            </div>
          </div>
        </div>

        <div class="col-form">
            <form
              name="contact"
              method="POST"
              action="/"
              data-netlify="true"
              netlify-honeypot="bot-field"
              @submit.prevent="submitForm"
              class="contact-form"
            >
            <input type="hidden" name="form-name" value="contact" />
            <input type="hidden" name="bot-field" />
            <div class="form-group">
              <label for="name">姓名</label>
              <input type="text" id="name" name="name" v-model="form.name" required placeholder="您的姓名">
            </div>
            <div class="form-group">
              <label for="email">Email</label>
              <input type="email" id="email" name="email" v-model="form.email" required placeholder="您的 Email">
            </div>
            <div class="form-group">
              <label for="subject">主旨</label>
              <input type="text" id="subject" name="subject" v-model="form.subject" required placeholder="專案詢問">
            </div>
            <div class="form-group">
              <label for="message">訊息</label>
              <textarea id="message" name="message" v-model="form.message" required rows="5" placeholder="我們能為您做什麼？"></textarea>
            </div>
            <button type="submit" class="btn-submit" :disabled="loading">
              {{ loading ? '送出中…' : '發送訊息' }}
            </button>
            <p v-if="success" class="form-success">訊息已送出，我們會盡快回覆您。</p>
            <p v-if="error" class="form-error">送出失敗，請稍後再試。</p>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const loading = ref(false)
const success = ref(false)
const error = ref(false)

function encode(data) {
  return new URLSearchParams(data).toString()
}

const submitForm = async () => {
  loading.value = true
  success.value = false
  error.value = false

  try {
    const body = encode({
      'form-name': 'contact',
      ...form
    })

    const res = await fetch('/', {
      method: 'POST',
      headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
      body
    })

    if (!res.ok) throw new Error('Submit failed')

    success.value = true

    // ✅ 送出成功後清空表單
    Object.assign(form, {
      name: '',
      email: '',
      subject: '',
      message: ''
    })

    // ✅ 5 秒後自動隱藏成功訊息
    setTimeout(() => {
      success.value = false
    }, 3000)

  } catch (e) {
    error.value = true

    // ❌ 5 秒後自動隱藏錯誤訊息
    setTimeout(() => {
      error.value = false
    }, 3000)

  } finally {
    loading.value = false
  }
}

</script>


<style lang="scss" scoped>
@import '../styles/main.scss';

.page-header {
  background-color: $primary-color;
  color: $white;
  padding: 4rem 0;
  text-align: center;
  margin-bottom: 4rem;

  h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
  }

  p {
    font-size: 1.2rem;
    opacity: 0.9;
  }
}

.content-section {
  padding-bottom: 4rem;
}

.row {
  display: flex;
  flex-direction: column;
  gap: 4rem;

  @media (min-width: $bp-md) {
    flex-direction: row;
  }
}

.col-info {
  flex: 1;

  h2 {
    color: $primary-color;
    margin-bottom: 1.5rem;
    font-size: 2rem;
  }

  .intro {
    color: #666;
    margin-bottom: 2.5rem;
    font-size: 1.1rem;
    line-height: 1.6;
  }
}

.contact-details {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;

  @media (min-width: $bp-sm) {
    grid-template-columns: repeat(2, 1fr);
  }

  .detail-item {
    h3 {
      font-size: 1.1rem;
      color: $secondary-color;
      margin-bottom: 0.5rem;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    p {
      color: #333;
      font-weight: 500;
    }
  }
}

.col-form {
  flex: 1;
  background: $white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
}

.contact-form {
  .form-group {
    margin-bottom: 1.5rem;

    label {
      display: block;
      margin-bottom: 0.5rem;
      font-weight: 600;
      color: $text-color;
    }

    input, textarea {
      width: 100%;
      padding: 0.8rem;
      border: 1px solid #ddd;
      border-radius: 4px;
      font-family: inherit;
      font-size: 1rem;
      transition: border-color 0.3s;

      &:focus {
        outline: none;
        border-color: $secondary-color;
      }
    }
  }

  .btn-submit {
    width: 100%;
    padding: 1rem;
    background-color: $secondary-color;
    color: $white;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    font-weight: 600;
    text-transform: uppercase;
    cursor: pointer;
    transition: background-color 0.3s;

    &:hover {
      background-color: darken($secondary-color, 10%);
    }
  }
    .form-success,
    .form-error {
      margin-top: 1rem;
      padding: 0.9rem 1rem;
      border-radius: 6px;
      font-weight: 600;
      font-size: 0.95rem;
      line-height: 1.4;
    }

    .form-success {
      background: rgba(46, 204, 113, 0.12);
      border: 1px solid rgba(46, 204, 113, 0.35);
      color: #1e7e34;
    }

    .form-error {
      background: rgba(231, 76, 60, 0.12);
      border: 1px solid rgba(231, 76, 60, 0.35);
      color: #b02a37;
    }

    .btn-submit:disabled {
      opacity: 0.65;
      cursor: not-allowed;
    }


}
</style>
