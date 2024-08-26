<template>
  <div class="w-screen mt-64 flex flex-col justify-center items-center gap-2">
    <div class="text-2xl mb-2">
      Se connecter
    </div>
    <div class="flex justify-center items-center w-full">
      <form>
        <ruby class="text-2xl">
          <input type="text" class="rounded border border-neutral-500 text-xl">
          <rp>(</rp>
          <rt>Identifiant/Email</rt>
          <rp>)</rp>
        </ruby>
      </form>
    </div>
    <div class="flex justify-center items-center w-full">
      <form>
        <ruby class="text-2xl">
          <input type="password" class="rounded border border-neutral-500 text-xl">
          <rp>(</rp>
          <rt>Password</rt>
          <rp>)</rp>
        </ruby>
      </form>
    </div>
    <button class="border-blue-200 border rounded shadow px-1 py-0.5 bg-blue-50">Valider</button>
  </div>
</template>

<script lang="ts">
definePageMeta({
  layout: 'login'
})
</script>