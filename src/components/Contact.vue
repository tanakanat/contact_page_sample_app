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

      <transition>
        <div
          v-if="isShowAlertBox"
          class="mb-3 py-2 text-center alert-danger rounded"
        >
          <span>
            入力に誤りがあるか、未入力になっています。<br />
            下記について再度ご確認のうえ、修正してください。
          </span>
        </div>
      </transition>

      <ContactInput
        id="conpanyName"
        type="text"
        label="会社名"
        :value="conpanyName"
        placeHolder="FooBar株式会社"
        :validationMessage="validationMessageConpanyName"
        @changeValue="changeConpanyName"
      />

      <ContactInput
        id="contactPersonName"
        type="text"
        label="担当者名"
        :value="contactPersonName"
        placeHolder="山田太郎"
        :validationMessage="validationMessageContactPersonName"
        @changeValue="changeContactPersonName"
      />

      <ContactInput
        id="mail"
        type="email"
        label="メールアドレス"
        :value="mail"
        placeHolder="foo@example.co"
        :validationMessage="validationMessageMail"
        @changeValue="changeMail"
      />

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

      <transition>
        <ContactInput
          v-if="isSelectedMaintenanceInfo"
          id="contractNumber"
          type="text"
          label="契約番号（数字4ケタ）"
          :value="contractNumber"
          placeHolder="1234"
          :validationMessage="validationMessageContractNumber"
          @changeValue="changeContractNumber"
        />
      </transition>

      <div class="mb-3">
        <label for="content" class="form-label"
          >お問い合わせ要件（255文字まで）</label
        >
        <span v-if="!!validationMessageContent" class="ml-2 text-danger rounded"
          >[!]{{ validationMessageContent }}</span
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
        <button
          type="button"
          class="btn btn-primary btn-lg"
          @click="clickSubmitButton"
        >
          送信する
        </button>
      </div>
    </main>
  </div>
</template>

<script>
import ContactInput from "./ContactInput";

export default {
  name: "Contact",
  components: {
    ContactInput,
  },
  data() {
    return {
      conpanyName: "", // 会社名
      contactPersonName: "", // 担当者名
      mail: "", // メールアドレス
      category: "", // お問い合わせ分類
      contractNumber: "", // 契約番号（数字4ケタ）
      content: "", // お問い合わせ要件（255文字まで）
      isShowAlertBox: false,
      validationMessageConpanyName: "",
      validationMessageContactPersonName: "",
      validationMessageMail: "",
      validationMessageContractNumber: "",
      validationMessageContent: "",
    };
  },
  computed: {
    isSelectedMaintenanceInfo() {
      return this.category === "maintenanceInfo";
    },
    isValidForm() {
      return !(
        this.validationMessageConpanyName ||
        this.validationMessageContactPersonName ||
        this.validationMessageMail ||
        this.validationMessageContractNumber ||
        this.validationMessageContent
      );
    },
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
    clickSubmitButton() {
      this.validateForm();

      if (!this.isValidForm) {
        this.isShowAlertBox = true;
        return;
      }
      this.submit();
    },
    submit() {
      console.log("submit"); // TODO: 実装
    },
    validateForm() {
      this.validateConpanyName();
      this.validateContactPersonName();
      this.validateMail();
      this.validateContractNumber();
      this.validateContent();
    },
    validateConpanyName() {
      if (this.conpanyName.length === 0) {
        this.validationMessageConpanyName = "会社名は必須です。";
      } else if (this.conpanyName.length > 64) {
        this.validationMessageConpanyName =
          "会社名は64文字以内で入力してください。";
      } else {
        this.validationMessageConpanyName = "";
      }
    },
    validateContactPersonName() {
      if (this.contactPersonName.length === 0) {
        this.validationMessageContactPersonName = "担当者名は必須です。";
      } else if (this.contactPersonName.length > 64) {
        this.validationMessageContactPersonName =
          "担当者名は64文字以内で入力してください。";
      } else {
        this.validationMessageContactPersonName = "";
      }
    },
    validateMail() {
      const mailRegExp =
        /^[A-Za-z0-9]{1}[A-Za-z0-9_.-]*@{1}[A-Za-z0-9_.-]+.[A-Za-z0-9]+$/;

      if (this.mail.length === 0) {
        this.validationMessageMail = "メールアドレスは必須です。";
      } else if (!mailRegExp.test(this.mail)) {
        this.validationMessageMail =
          "メールアドレスを正しい形式で入力してください。";
      } else {
        this.validationMessageMail = "";
      }
    },
    validateContractNumber() {
      if (this.category !== "maintenanceInfo") {
        this.validationMessageContractNumber = "";
        return;
      }

      const contractNumberRegExp = /^[0-9]{4}$/;

      if (this.contractNumber.length === 0) {
        this.validationMessageContractNumber = "契約番号は必須です。";
      } else if (!contractNumberRegExp.test(this.contractNumber)) {
        this.validationMessageContractNumber =
          "契約番号を数字4ケタで入力してください。";
      } else {
        this.validationMessageContractNumber = "";
      }
    },
    validateContent() {
      if (this.content.length === 0) {
        this.validationMessageContent = "お問い合わせ要件は必須です。";
      } else if (this.content.length > 255) {
        this.validationMessageContent =
          "お問い合わせ要件は255文字以内で入力してください。";
      } else {
        this.validationMessageContent = "";
      }
    },
  },
};
</script>

<style scoped>
/* アニメーション中のスタイル */
.v-leave-active,
.v-enter-active {
  transition: opacity 0.2s;
}

/* 表示アニメーション */
.v-enter {
  opacity: 0;
}
.v-enter-to {
  opacity: 1;
}

/* 非表示アニメーション */
.v-leave {
  opacity: 1;
}
.v-leave-to {
  opacity: 0;
}
</style>
