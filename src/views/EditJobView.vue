<script setup>
import { reactive, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";
import { useToast } from "vue-toastification";
import axios from "axios";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import JobForm from "@/components/JobForm.vue";

const toast = useToast();
const route = useRoute();
const router = useRouter();

const jobId = route.params.id;

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

const state = reactive({
  job: {},
  isLoading: true,
});

const submitForm = async () => {
  try {
    const updatedJob = {
      ...form,
      company: {
        ...form.company,
      },
    };
    await axios.put(`/api/jobs/${jobId}`, updatedJob);
    toast.success("Job Updated Successfully");
    router.push(`/jobs/${jobId}`);
  } catch (error) {
    console.error("Error updating a job. ", error);
    toast.error("Error Updating a Job");
  }
};

onMounted(async () => {
  try {
    const response = await axios.get(`/api/jobs/${jobId}`);
    state.job = response.data;
    Object.assign(form, { ...state.job, company: { ...state.job.company } });
  } catch (error) {
    console.error("Error fetching a job. ", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <JobForm
    v-if="!isLoading"
    :form="form"
    :onSubmit="submitForm"
    title="Edit Job"
    buttonText="Edit Job"
  />

  <div v-else>
    <PulseLoader />
  </div>
</template>
