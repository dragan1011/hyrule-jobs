<template>
	<div class="job-list">
		<p>Ordered by {{ order }}</p>
		<transition-group name="list" tag="ul">
			<li v-for="job in orderedJobs" :key="job.id">
				<h2>{{ job.title }} in {{ job.location }}</h2>
				<div class="salary">
					<img src="../assets/rupee.svg" alt="Rupee">
					<p>{{ job.salary }} rupees</p>
				</div>
				<div class="description">
					<p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Repellendus aspernatur saepe autem aliquid culpa qui voluptas cupiditate debitis officia? Tenetur consectetur hic aperiam harum nostrum id cupiditate porro qui provident?</p>
				</div>
			</li>
		</transition-group>
	</div>
</template>
<script lang="ts">
import { defineComponent, PropType, computed } from 'vue';
import Job from '@/types/Job'
import OrderTerms from '@/types/OrderTerms';

export default defineComponent({
	props: {
		jobs: {
			reqired: true,
			type: Array as PropType<Job[]>
		},
		order: {
			required: true,
			type: String as PropType<OrderTerms>
		}
	},
	setup(props) {
		const orderedJobs = computed(() => {
			return [...props.jobs].sort((a: Job, b: Job) =>{
				return a[props.order] > b[props.order] ? 1 : -1
			})
		})

		return { orderedJobs }
	}
})

</script>

<style scoped>
  .job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
	transition: 300ms;
  }

  .job-list li:hover{
	transform: scale(1.015);
	transition: 300ms;
	cursor: default;
  }

  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move{
	transition: all 1s;
  }
</style>