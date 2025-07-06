<script setup>
import { reactive } from "vue";
import { useRouter } from "vue-router";
import { useToast } from "vue-toastification";
import axios from "axios";
import JobForm from "@/components/JobForm.vue";

const form = reactive({
  type: "Full-Time",
  title: "",
  description: "",
  salary: "",
  location: "",
  company: {
    name: "",
    description: "",
    contactEmail: "",
    contactPhone: "",
  },
});

const toast = useToast();
const router = useRouter();

const submitForm = async () => {
  try {
    const newJob = {
      ...form,
      company: {
        ...form.company,
      },
    };
    const response = await axios.post("/api/jobs", newJob);
    toast.success("Job Added Successfully");
    router.push(`/jobs/${response.data.id}`);
  } catch (error) {
    console.error("Error adding job. ", error);
    toast.error("Error Adding a Job");
  }
};
</script>

<template>
  <JobForm :form="form" :onSubmit="submitForm" />
</template>
