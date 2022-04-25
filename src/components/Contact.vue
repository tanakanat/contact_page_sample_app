<template>
  <div class="container">
    <main class="my-5">
      <div class="pb-3 text-center">
        <h2>お問い合わせフォーム</h2>
        <p class="lead">
          お客さまからのご質問をお問い合わせフォームにて受け付けております。<br />
          必要事項をご記入の上、「送信する」ボタンを押してください。
        </p>
      </div>

      <div class="mb-3">
        <label for="conpanyName" class="form-label">会社名</label>
        <input
          type="text"
          class="form-control"
          id="conpanyName"
          placeholder="FooBar株式会社"
        />
      </div>

      <div class="mb-3">
        <label for="contactPerson" class="form-label">担当者名</label>
        <input
          type="text"
          class="form-control"
          id="contactPerson"
          placeholder="山田太郎"
        />
      </div>

      <div class="mb-3">
        <label for="mail" class="form-label">メールアドレス</label>
        <input
          type="email"
          class="form-control"
          id="mail"
          placeholder="foo@example.com"
        />
      </div>

      <div class="mb-3">
        <label for="category" class="mr-2 form-label">お問い合わせ分類</label>
        <select class="form-select" id="category" required>
          <option value="">選択</option>
          <option>仕様</option>
          <option>契約</option>
          <option>メンテナンス情報</option>
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
        />
      </div>

      <div class="mb-3">
        <label for="content" class="form-label"
          >お問い合わせ要件（255文字まで）</label
        >
        <textarea class="form-control" id="content" rows="3"></textarea>
      </div>

      <div class="text-center">
        <button type="button" class="btn btn-primary btn-lg">送信する</button>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "Contact",
};
</script>

<style scoped>
</style>
