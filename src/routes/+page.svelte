<script lang="ts">
	import { resolve } from '$app/paths';
	import { ArrowRight, Circle } from '@lucide/svelte';

	const title = 'path2ttf — Convert SVG Icons to PUA-Mapped TTF Fonts';
	const description =
		'Offline-first web app to convert Lucide, Tabler, or custom stroked SVG icons into filled-path TrueType (TTF) fonts mapped to Unicode Private Use Area codepoints.';
	const canonicalUrl = 'https://path2ttf.pages.dev/';

	const jsonLd = JSON.stringify({
		'@context': 'https://schema.org',
		'@type': 'SoftwareApplication',
		name: 'path2ttf',
		applicationCategory: 'DeveloperApplication',
		operatingSystem: 'Any (Web / PWA)',
		offers: { '@type': 'Offer', price: '0', priceCurrency: 'USD' },
		description,
		url: canonicalUrl
	});

	// Some quircky stuff :)
	const jsonld_str = '<script type="application/ld+json">' + jsonLd + '</scr' + 'ipt>';

	interface IStep {
		title: string;
		description: string;
		img: string;
	}

	// Steps
	const stepData: IStep[] = [
		{
			title: 'Pick or Upload SVGs',
			description:
				'Grab icons from Lucide or Tabler, or drop in your own SVG files. Everything stays saved right in your browser.',
			img: 'step-1-pick-upload-svg.svg'
		},
		{
			title: 'Configure and Generate Your Font',
			description:
				'Turns thin line icons into solid shapes, sets your font name and size rules, gives each icon a code, and downloads a TTF file.',
			img: 'step-2-stroke-to-font-config.svg'
		},
		{
			title: 'Preview & Use Your Font',
			description:
				'Test your TTF right on the page—even one you already had—and click to copy icon codes for your project.',
			img: 'step-3-pua-glyph-preview.svg'
		}
	];
</script>

<svelte:head>
	<title>{title}</title>
	<meta name="description" content={description} />
	<link rel="canonical" href={canonicalUrl} />

	<meta property="og:title" content={title} />
	<meta property="og:description" content={description} />
	<meta property="og:url" content={canonicalUrl} />
	<meta property="og:image" content="{canonicalUrl}og-path2ttf.png" />
	<meta name="twitter:card" content="summary_large_image" />

	<!-- eslint-disable-next-line svelte/no-at-html-tags -->
	{@html jsonld_str}
</svelte:head>

<div class="flex min-h-screen flex-col bg-surface text-on-surface">
	<a
		href="#main-content"
		class="sr-only focus:not-sr-only focus:fixed focus:top-4 focus:left-4 focus:z-50 focus:rounded-md focus:bg-primary focus:px-4 focus:py-2 focus:font-body focus:text-sm focus:font-semibold focus:text-on-primary"
	>
		Skip to main content
	</a>

	<header class="border-b-2 border-outline-variant bg-surface-container-low">
		<div class="container mx-auto flex items-center justify-between px-6 py-4">
			<a
				class="inline-flex items-center rounded-sm focus-visible:ring-2 focus-visible:ring-primary focus-visible:outline-none"
				href={resolve('/')}
				aria-label="path2ttf home"
			>
				{@render logo('text-xl')}
			</a>

			<nav aria-label="Primary">
				<a
					href={resolve('/app')}
					class="btn bg-surface-container text-sm font-medium transition hover:brightness-110 focus-visible:ring-2 focus-visible:ring-primary focus-visible:outline-none active:scale-95"
				>
					Go to App <ArrowRight class="h-4 w-4" aria-hidden="true" />
				</a>
			</nav>
		</div>
	</header>

	<main id="main-content" class="flex-1">
		<div class="container mx-auto px-4">
			<section aria-labelledby="hero-heading" class="grid items-center gap-8 py-16 md:grid-cols-2">
				<div class="order-1 text-center md:order-0 md:text-left">
					<h1 id="hero-heading" class="font-title text-5xl font-extrabold">
						SVGs to clean <br class="hidden md:block" /> TTF fonts.
					</h1>
					<p class="text-body-md my-4 max-w-prose font-body text-pretty text-on-surface-variant">
						Pick icons from Lucide or Tabler, or upload your own SVGs. Convert strokes to filled
						paths, configure your font, and map glyphs to Unicode PUA.
					</p>
					<a
						class="btn mx-auto bg-primary font-semibold text-on-primary transition hover:brightness-110 focus-visible:ring-2 focus-visible:ring-primary focus-visible:ring-offset-2 focus-visible:ring-offset-surface focus-visible:outline-none active:scale-95 md:mx-0"
						href={resolve('/app')}
					>
						Go to App <ArrowRight class="h-5 w-5" aria-hidden="true" />
					</a>
				</div>

				<div class="order-0 md:order-1">
					<img
						src="/images/hero-svg-to-ttf.svg"
						alt="Stroked SVG icons converting into a PUA-mapped TTF font"
						width="480"
						height="340"
						fetchpriority="high"
						class="h-auto w-full object-contain"
					/>
				</div>
			</section>

			<section aria-labelledby="hero-heading" class="py-16">
				<div class="text-center">
					<h2 id="hero-heading" class="font-title text-4xl font-bold">
						How It Works in Three Simple Steps
					</h2>
					<p
						class="text-body-md mx-auto my-4 max-w-prose font-body text-pretty text-on-surface-variant"
					>
						Pick / Upload icons, configure the font, preview / export the PUA mapped TTF.
					</p>
				</div>
				<div class="mt-16">
					{#each stepData as s, idx (idx)}
						{@render step(s, idx, stepData.length)}
					{/each}
				</div>
			</section>
		</div>
	</main>

	<footer class="border-t-2 border-outline-variant bg-surface-container-low">
		<div class="container mx-auto flex items-center justify-center gap-2 px-6 py-4">
			{@render logo('text-xs')}
			<span class="mx-0.5 font-mono font-extrabold opacity-45" aria-hidden="true">|</span>
			<span class="text-xs font-medium text-tertiary">
				Built with <span role="img" aria-label="love">❤️</span> by
				<a
					target="_blank"
					rel="noopener noreferrer"
					class="rounded-sm underline focus-visible:ring-2 focus-visible:ring-primary focus-visible:outline-none"
					href="https://github.com/akryptic"
				>
					Akryptic
				</a>
			</span>
		</div>
	</footer>
</div>

{#snippet logo(className?: string)}
	<span
		class="font-mono font-semibold tracking-wide {className ? className : ''}"
		aria-hidden="true"
	>
		path2<span class="ml-1 inline-block text-primary">ttf</span>
	</span>
{/snippet}

{#snippet step({ title, description, img }: IStep, idx: number, stepCount: number)}
	<!-- Ignore the comments, I couldn't come up with good names for these sections :p -->
	<div
		class="grid grid-cols-[auto_1fr] grid-rows-2 gap-x-6 md:grid-cols-[1fr_auto_1fr] md:grid-rows-1"
	>
		<!-- Step details -->
		<div
			class="p-4 pb-0 {idx % 2 ? 'md:order-1' : 'md:-order-1'} {idx != stepCount - 1
				? 'pb-16'
				: ''}"
		>
			<span
				class="rounded bg-primary-container px-2 py-1 text-xs font-semibold text-on-primary-container"
			>
				Step {idx + 1}
			</span>
			<h3 class="my-2 font-title text-xl font-bold">{title}</h3>
			<p class="text-on-surface-variant">{description}</p>
		</div>

		<!-- Progression Line -->
		<div
			class="relative -order-1 row-span-2 w-0.75 bg-primary text-primary md:order-0 {idx ==
			stepCount - 1
				? 'h-14'
				: 'h-full'}"
		>
			<Circle fill="currentColor" class="absolute top-5 left-1/2 size-4 -translate-x-1/2" />
		</div>

		<!-- Step Image -->
		<div class="px-4 {idx % 2 ? 'md:-order-1 md:ml-auto' : ' md:order-1'} ">
			<div class="w-fit overflow-hidden rounded border border-outline bg-surface-container-low p-1">
				<img src="/images/{img}" alt="" />
			</div>
		</div>
	</div>
{/snippet}
