<template>
  <h2>Job list</h2>
  <p> order by {{order}}</p>
  <ul>
    <li v-for="job in orderedJobs" :key="job.id ">
      <h2>{{job.title}} in {{job.location}}</h2>
      <div class="salary">
        <p>{{job.salary}} dolor</p>
      </div>
      <div class="description">
        <p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Animi, aperiam atque autem deleniti ducimus error excepturi iure minus neque non nulla porro provident quod rem, rerum tempora vel veritatis voluptatem.
        </p>
      </div>
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent ,PropType , computed  } from "vue";
import Job from "@/types/Job";
import OrderTerm from "@/types/OrderTerm";
export default defineComponent({
  name: "JobList",
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order:{
      required: true,
      type: String as PropType<OrderTerm>
    }
  },
  setup(props)  {
    const orderedJobs =  computed(() =>{
      return [...props.jobs].sort((a: Job, b: Job)=> {
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })
    return { orderedJobs}
  }
});
</script>
