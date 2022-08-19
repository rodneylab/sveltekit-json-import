<script>
	// import entire JSON file as a default import
	import people from '$lib/data/people.json';

	// import root level object as a named import
	import { sponsors } from '$lib/data/clientsSponsors.json';

	import '@fontsource/open-sans/400.css';
	import '@fontsource/open-sans/700.css';

	const BULLET_ENTITY = '\u2022';
	const EM_SPACE_ENTITY = '\u2003';

	// we access the root level sponsors element (which is an array) directly in code
	const sponsorString = sponsors
		.map((element) => element.name)
		.join(`${EM_SPACE_ENTITY}${BULLET_ENTITY}${EM_SPACE_ENTITY}`);
</script>

<svelte:head>
	<title>About Us</title>
	<html lang="en-GB" />
</svelte:head>

<header class="heading">
	<div class="title">
		<h1>About Us</h1>
	</div>
</header>
<main>
	<section class="sponsors">
		<h2>Our Sponsors</h2>
		<div class="scrolling-text"><p>{sponsorString}</p></div>
	</section>
	<section>
		<h2>Our People</h2>
		<div class="people">
			<!-- We can access the people default import which is an array directly in the code -->
			{#each people as { firstName, lastName, jobTitle, email }, index}
				<article aria-posinset={index + 1} aria-setsize={people.length} class="person">
					<h2>{firstName} {lastName}</h2>
					<p><strong>{jobTitle}</strong></p>
					<p>{email}</p>
				</article>
			{/each}
		</div>
	</section>
</main>

<style>
	:global(html) {
		font-family: Open Sans;
		background: #ffca3a;
	}
	h1 {
		font-size: 3.052rem;
	}
	h2 {
		font-size: 1.953rem;
		padding-top: 2rem;
		padding-left: 3rem;
	}
	h1,
	h2 {
		color: #395c6b;
	}
	.heading {
		display: flex;
		justify-content: center;
		margin: 3rem auto;
	}
	.title {
		border: 0.25rem solid #ff595e;
		border-radius: 1rem;
		padding: 0 2rem;
	}
	.sponsors {
		margin-bottom: 3rem;
	}
	.scrolling-text {
		height: 3rem;
		position: relative;
		white-space: nowrap;
		color: #395c6b;
	}

	.scrolling-text p {
		position: absolute;
		width: fit-content;
		height: 100%;
		margin: 0;
		line-height: 3rem;
		text-align: center;
		font-size: 2.441rem;
		transform: translateX(100%);
		animation: scroll-text 45s linear infinite;
	}

	@keyframes scroll-text {
		0% {
			transform: translateX(25%);
		}
		100% {
			transform: translateX(-100%);
		}
	}

	.people {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		column-gap: 2rem;
		row-gap: 2rem;
		padding: 1.5rem 3rem 3rem;
	}

	.person {
		background: #8ac926;
		border: 0.25rem solid #1982c4;
		box-shadow: 0.25rem 0.25rem #6a4c9380;
		border-radius: 1rem;
		padding: 0.5rem 1rem;
	}

	.person h2 {
		padding-left: 0;
		margin-bottom: 0.5rem;
		padding-top: 0.5rem;
		font-size: 1.563rem;
	}

	.person h2,
	.person p {
		margin-top: 0.25rem;
	}

	@media (max-width: 768px) {
		.people {
			grid-template-columns: 1fr;
		}
	}
</style>
