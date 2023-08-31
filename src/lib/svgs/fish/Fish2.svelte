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
	transform="translate({translate.join(' ')})rotate({rotate})scale({scale.join(', ')})"
	d="M220 85.1a10 10 0 0 0-4.5-8.3 46 46 0 0 0-48.4 0 54 54 0 0 0-9 6.7A104.4 104.4 0 0 0 95 60C50 60 26.3 97.4 20 117.1a11.4 11.4 0 0 0 0 5.8C26.3 142.6 50 180 95 180a104.4 104.4 0 0 0 63.1-23.7 60.7 60.7 0 0 0 9 6.8 46.2 46.2 0 0 0 48.4 0 10 10 0 0 0 4.5-8.3A54.3 54.3 0 0 0 205.8 120 54.3 54.3 0 0 0 220 85.1Z"
/>
