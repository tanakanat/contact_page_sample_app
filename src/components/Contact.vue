<template>
  <div class="container">
    <main class="my-5">
      <div class="pb-3 text-center">
        <h2>お問い合わせフォーム</h2>
        <span>
          お客さまからのご質問をお問い合わせフォームにて受け付けております。<br />
          必要事項をご記入の上、「送信する」ボタンを押してください。
        </span>
      </div>

      <div
        v-if="!isFormValid"
        class="mb-3 py-2 text-center alert-danger rounded"
      >
        <span>
          入力に誤りがあるか、未入力になっています。<br />
          下記について再度ご確認のうえ、修正してください。
        </span>
      </div>

      <div class="mb-3">
        <label for="conpanyName" class="form-label">会社名</label>
        <input
          type="text"
          class="form-control"
          id="conpanyName"
          placeholder="FooBar株式会社"
          :value="conpanyName"
          @input="changeConpanyName"
        />
      </div>

      <div class="mb-3">
        <label for="contactPersonName" class="form-label">担当者名</label>
        <input
          type="text"
          class="form-control"
          id="contactPersonName"
          placeholder="山田太郎"
          :value="contactPersonName"
          @input="changeContactPersonName"
        />
      </div>

      <div class="mb-3">
        <label for="mail" class="form-label">メールアドレス</label>
        <input
          type="email"
          class="form-control"
          id="mail"
          placeholder="foo@example.com"
          :value="mail"
          @input="changeMail"
        />
      </div>

      <div class="mb-3">
        <label for="category" class="mr-2 form-label">お問い合わせ分類</label>
        <select
          class="form-select"
          id="category"
          required
          :value="category"
          @input="changeCategory"
        >
          <option value="">選択</option>
          <option value="specification">仕様</option>
          <option value="contract">契約</option>
          <option value="maintenanceInfo">メンテナンス情報</option>
        </select>
      </div>

      <div class="mb-3">
        <label for="contractNumber" class="form-label"
          >契約番号（数字4ケタ）</label
        >
        <input
          type="text"
          class="form-control"
          id="contractNumber"
          placeholder="1234"
          :value="contractNumber"
          @input="changeContractNumber"
        />
      </div>

      <div class="mb-3">
        <label for="content" class="form-label"
          >お問い合わせ要件（255文字まで）</label
        >
        <textarea
          class="form-control"
          id="content"
          rows="3"
          :value="content"
          @input="changeContent"
        ></textarea>
      </div>

      <div class="text-center">
        <button type="button" class="btn btn-primary btn-lg" @click="submit">
          送信する
        </button>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "Contact",
  data() {
    return {
      conpanyName: "", // 会社名
      contactPersonName: "", // 担当者名
      mail: "", // メールアドレス
      category: "", // お問い合わせ分類
      contractNumber: "", // 契約番号（数字4ケタ）
      content: "", // お問い合わせ要件（255文字まで）
      isFormValid: true,
    };
  },
  methods: {
    changeConpanyName(ev) {
      this.conpanyName = ev.target.value;
    },
    changeContactPersonName(ev) {
      this.contactPersonName = ev.target.value;
    },
    changeMail(ev) {
      this.mail = ev.target.value;
    },
    changeCategory(ev) {
      this.category = ev.target.value;
    },
    changeContractNumber(ev) {
      this.contractNumber = ev.target.value;
    },
    changeContent(ev) {
      this.content = ev.target.value;
    },
    submit() {
      this.validateForm();
    },
    validateForm() {
      this.isFormValid = false;
    },
  },
};
</script>

<style scoped>
</style>
