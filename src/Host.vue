<template>
  loading

</template>

<script setup lang="ts">
import { computed, reactive, ref, toRefs, onMounted } from "vue";
import axios from "axios";
import {useHostStore} from "@/stores/host";


const pageData = reactive({
	host: 'https://1254205949-08q19onj0f.ap-guangzhou.tencentscf.com',
  loading: false,
  error: false
})

const {setHost} = useHostStore()

const baseUrl = computed(() => {
  return pageData.host.trimEnd('/')
})

const sub = async () => {
  pageData.loading = true
  try {
    await axios.get(baseUrl.value + '/banner')
    setHost(baseUrl.value)
  } catch (e) {
    pageData.error = true
    setTimeout(() => {
      pageData.error = false
    }, 5000)
  }
  pageData.loading = false
}

onMounted(() => {
	console.log("mounted");
	sub();
})

</script>
