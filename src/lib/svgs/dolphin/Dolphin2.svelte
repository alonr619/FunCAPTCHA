<script lang="ts">
	export let color: string = '#fff';
	export let id: string = '';
	export let className: string = '';
	export let translate: number[] = [0, 0];
	export let rotate: number = 0;
	export let scale: number[] = [1, 1];
</script>

<path
	class="icon {className}"
	fill={color}
	id="#{id}"
	transform="translate({translate.join(' ')})rotate({rotate})scale({scale
		.map((el) => el * 2)
		.join(', ')})"
	d="M86.2,31.5c-1.8-1.8-3.8-2.8-8-4.1c0,0,0-25.9-20.4-25.9c-7.2,0-13.9,1.7-19.9,4.7C35.6,5.1,26.4,1.4,15.7,4
	c-1.9,0.5-2.2,3.1-0.4,3.9c3.3,1.6,6.8,4.8,6.8,11.3c-5.7,7.5-9.1,16.8-9.1,27c0,24.7,20,44.6,44.7,44.6c0,0,7.1,2.2,10.7,6.9
	c1.1,1.4,3.3,0.6,3.2-1.1c-0.2-3.2-1.6-7.2-5.6-11.3c4.1-4.1,5.4-8.1,5.6-11.3c0.1-1.7-2.1-2.5-3.2-1.1c-3.6,4.8-10.6,7.2-10.6,7.2
	c-12.4,0-22.3-10-22-22.5c0.3-12.1,10.6-21.5,22.6-21.5h25.5C86.5,36.2,87.9,33.3,86.2,31.5z M30.9,49.9c0,0-9.6,0.3-9.6-9.3v-1.7
	c0-3.3,2.7-6,6-6h3.6V49.9z M52.2,57.8v-16c-4,1.5-7.4,4.3-9.5,7.9C43.5,58.1,52.2,57.8,52.2,57.8z"
/>
