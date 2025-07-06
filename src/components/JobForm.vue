<script setup>
import { jobTypes, salaryRanges } from "@/constants/jobOptions";

defineProps({
  form: Object,
  onSubmit: Function,
  title: { type: String, default: "Add Job" },
  buttonText: { type: String, default: "Add Job" },
});
</script>

<template>
  <section class="bg-green-50">
    <div class="container m-auto max-w-2xl py-24">
      <div
        class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0"
      >
        <form @submit.prevent="onSubmit">
          <h2 class="text-3xl text-center font-semibold mb-6">{{ title }}</h2>

          <div class="mb-4">
            <label for="type" class="block text-gray-700 font-bold mb-2"
              >Job Type</label
            >
            <select
              v-model="form.type"
              class="border rounded w-full py-2 px-3"
              required
            >
              <option
                v-for="jobType of jobTypes"
                :key="jobType"
                :value="jobType"
              >
                {{ jobType }}
              </option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Job Listing Name</label
            >
            <input
              v-model="form.title"
              type="text"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="eg. Beautiful Apartment In Miami"
              required
            />
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Description</label
            >
            <textarea
              v-model="form.description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="Add any job duties, expectations, requirements, etc"
            ></textarea>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2">Salary</label>
            <select
              v-model="form.salary"
              class="border rounded w-full py-2 px-3"
              required
            >
              <option
                v-for="salary of salaryRanges"
                :key="salary"
                :value="salary"
              >
                {{ salary }}
              </option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2">Location</label>
            <input
              v-model="form.location"
              type="text"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Company Location"
              required
            />
          </div>

          <h3 class="text-2xl mb-5">Company Info</h3>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Company Name</label
            >
            <input
              v-model="form.company.name"
              type="text"
              class="border rounded w-full py-2 px-3"
              placeholder="Company Name"
            />
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Company Description</label
            >
            <textarea
              v-model="form.company.description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="What does your company do?"
            ></textarea>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Contact Email</label
            >
            <input
              v-model="form.company.contactEmail"
              type="email"
              class="border rounded w-full py-2 px-3"
              placeholder="Email address for applicants"
              required
            />
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Contact Phone</label
            >
            <input
              v-model="form.company.contactPhone"
              type="tel"
              class="border rounded w-full py-2 px-3"
              placeholder="Optional phone for applicants"
            />
          </div>

          <div>
            <button
              class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline"
              type="submit"
            >
              {{ buttonText }}
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>
