<template>
	<v-data-table
		:items = "problemItem"
		:headers = "headers"
		:loading = "isLoading"
		hide-actions >
		<v-progress-linear
			slot = "progress"
			color = "primary"
			height = "5"
			indeterminate
		/>
		<template
			slot="items"
			slot-scope="props">
			<router-link
				:to = "{name: 'ProblemDetail', params: {slug: props.item.slug}}"
				:style = "{cursor: 'pointer'}"
				tile
				tag = "tr">
				<td class="text-xs-center">{{ props.item.pk }}</td>
				<td class="text-xs-center">
					<span>{{ props.item.title }}</span>
				</td>
				<td class="text-xs-center">{{ props.item.accept }}/{{ props.item.submit }}</td>
				<td class="text-xs-center">
					{{ (props.item.submit ? (props.item.accept / props.item.submit) * 100 : 0).toFixed(2) }}%
				</td>
			</router-link>
		</template>
	</v-data-table>
</template>

<script>
export default {
	props: {
		problemItem: {
			type: Array,
			default: () => [],
		},
		isLoading: {
			type: Boolean,
			default: false,
		},
	},


	data: () => ({
		hidden: false,
		headers: [
			{
				text: '#',
				align: 'center',
				sortable: false,
			},
			{
				text: 'Title',
				align: 'center',
				sortable: false,
			},
			{
				text: 'Accepted/Submit',
				align: 'center',
				sortable: false,
				class: 'hidden-sm-and-down',
			},
			{
				text: 'A/S',
				align: 'center',
				sortable: false,
				class: 'hidden-md-and-up',
			},
			{
				text: 'Ratio',
				align: 'center',
				sortable: false,
			},
		],
	}),
};
</script>
