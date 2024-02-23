<script lang="ts">
	import { onMount } from 'svelte';

	let isAnimating = 0;
	let isReverse = false;

	onMount(() => {
		const links = document.querySelectorAll('.hero-list a');
		const decorations = document.querySelectorAll('.hero-decoration img');

		const handleEnter = (event: any) => {
			isReverse = true;
			const selected = event.target.dataset.position;

			decorations.forEach((decoration) => {
				if (selected === decoration.dataset.position) {
					isAnimating = Number(selected);
				}
			});
		};

		const handleLeave = () => {
			isReverse = false;

			decorations.forEach((decoration) => {
				isAnimating = 0;
			});
		};

		links.forEach((link) => {
			link.addEventListener('mouseenter', handleEnter);
			link.addEventListener('mouseleave', handleLeave);
		});
	});
</script>

<div class="hero">
	<h1 class:is-reverse={isReverse}>Innovation driven holding company</h1>
	<ul class="hero-list" class:is-reverse={isReverse}>
		<li><a data-position="1" class:is-reverse={isReverse} href="#todo">Entertainment</a></li>
		<li><a data-position="2" href="#todo">Hospitality</a></li>
		<li><a data-position="3" href="#todo">Investments</a></li>
		<li><a data-position="4" href="#todo">Clean Energy</a></li>
		<li><a data-position="5" href="#todo">Real estate</a></li>
		<li><a data-position="6" href="#todo">Elements</a></li>
	</ul>
	<div class="hero-image">
		<img
			class:is-animating={isAnimating === 1}
			src="red-photo.jpg"
			srcset="red-photo@2x.jpg"
			alt="Obrázek"
		/>
		<img
			class:is-animating={isAnimating === 2}
			src="purple-photo.jpg"
			srcset="purple-photo@2x.jpg"
			alt="Obrázek"
		/>
		<img
			class:is-animating={isAnimating === 3}
			src="blue-photo.jpg"
			srcset="blue-photo@2x.jpg"
			alt="Obrázek"
		/>
		<img
			class:is-animating={isAnimating === 4}
			src="green-photo.jpg"
			srcset="green-photo@2x.jpg"
			alt="Obrázek"
		/>
		<img
			class:is-animating={isAnimating === 5}
			src="brown-photo.jpg"
			srcset="brown-photo@2x.jpg"
			alt="Obrázek"
		/>
		<img
			class:is-animating={isAnimating === 6}
			src="grey-photo.jpg"
			srcset="grey-photo@2x.jpg"
			alt="Obrázek"
		/>
	</div>
	<div class="hero-decoration">
		<img
			data-position="0"
			class:is-animating={isAnimating === 0}
			src="main-decoration.svg"
			alt="Dekorace"
		/>
		<img
			data-position="1"
			class:is-animating={isAnimating === 1}
			src="red-decoration.svg"
			alt="Dekorace"
		/>
		<img
			data-position="2"
			class:is-animating={isAnimating === 2}
			src="purple-decoration.svg"
			alt="Dekorace"
		/>
		<img
			data-position="3"
			class:is-animating={isAnimating === 3}
			src="blue-decoration.svg"
			alt="Dekorace"
		/>
		<img
			data-position="4"
			class:is-animating={isAnimating === 4}
			src="green-decoration.svg"
			alt="Dekorace"
		/>
		<img
			data-position="5"
			class:is-animating={isAnimating === 5}
			src="brown-decoration.svg"
			alt="Dekorace"
		/>
		<img
			data-position="6"
			class:is-animating={isAnimating === 6}
			src="grey-decoration.svg"
			alt="Dekorace"
		/>
	</div>
</div>

<style lang="stylus">
	.hero
		position relative
		display flex
		justify-content center
		flex-direction column
		height 100%
		padding 0 24px
		height 100vh
		overflow hidden
	
	.hero-image
		img
			position absolute
			inset 0
			height 100%
			width 100%
			object-fit cover
			z-index -2
			animation zoomIn 40s 1 ease;
			transition opacity 0.6s ease
			opacity 0

			&.is-animating
				opacity 1
		
	.hero-decoration
		img
			position absolute
			inset 0
			height 100%
			width 100%
			z-index -1
			transform scale(4)
			transition transform 2s $easeOutExpo, opacity 1s $easeOutExpo, filter 1s $easeOutExpo
			opacity 0
			filter blur(3px)
			object-fit cover
			transform-origin center
			animation slideIn 4s 1 $easeOutExpo

			&.is-animating
				transform scale(1)
				filter blur(0px)
				opacity 1

	h1
		color #9FBACB
		text-align center
		font-size 1.4rem
		line-height 34.67px
		margin (21/24em) 0
		letter-spacing (9.2/24em)
		text-transform uppercase
		animation headingSlide 4s 1 $easeOutExpo
		transition color .6s $easeOutExpo

		@media $medium-up
			font-size rvw(14, 24)
			
		@media $xlarge-up
			font-size 2.4rem
	
		&.is-reverse
			color #EFF3F6
		
	.hero-list
		list-style-type none
		padding-left 0
		display grid
		grid-template-columns repeat(2, 1fr)
		animation slideUp 4s 1 $easeOutExpo

		&.is-reverse
			li a
				color #FEFEFE

				&:hover
					&:before
						background white

				&:before
					background white
				
				&:after
					background white !important

		li:nth-child(1)
			@media $large-up
				position relative
				left (680/96em)
		
		li:nth-child(2)
			@media $large-up
				position relative
				left (680/96em)
		
		li:nth-child(5)
			@media $large-up
				position relative
				left (400/96em)
		
		li:nth-child(6)
			@media $large-up
				position relative
				left (400/96em)

		li:nth-child(even)
			a
				text-align left
				margin-left (36/96em)
		
		li:nth-child(odd)
			a
				position relative
				text-align right
				margin-right (36/96em)
				margin-left auto

				&:after
					content ""
					position absolute
					right (-40/96em)
					top 50%
					transform translateY(-50%)
					width (12/96em)
					height (12/96em)
					background #0C1D26
					transform skewX(0deg)
					transition background .6s $easeOutExpo

					@media $medium-up
						width (8/96em)
						height (8/96em)

		a
			display block
			font-weight 500
			line-height (128/96)
			font-size 2.5rem
			color #0C1D26
			text-decoration-color transparent
			transition text-decoration .6s $easeOutExpo
			text-underline-offset 19px
			text-decoration none
			position relative
			transition all .6s
			width max-content
	
			&:before
				content ""
				width 0
				height 0.075em
				position absolute
				bottom -3px
				left 0
				background #0C1D26
				transform skewX(0deg)
				transition all .6s
	
			&:hover
				transform skewX(-10deg)

				&:before
					width 100%
					left 0
				
				&:after
					transform skewX(10deg) !important
		
			@media $small-wide-up
				font-size rvw(25, 96, $fromMedia: $viewports.smallWide.min, $toMedia: $viewports.xlarge.max)
			
			@media $xxlarge-up
				font-size 9.6rem
		
	@keyframes headingSlide
		from
			transform translateY(40%)
			opacity 0
		to
			transform translateY(0%)
			opacity 1
	
	@keyframes slideUp
		from
			transform translateY(100%)
		to
			transform translateY(0%)
	
	@keyframes slideIn
		from
			transform scale(4)
		to
			transform scale(1)
	
	@keyframes zoomIn
		from
			transform scale(1)
		to
			transform scale(1.3)
</style>
