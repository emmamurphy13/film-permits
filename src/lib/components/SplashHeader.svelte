<!--
@component
SplashHeader.svelte — Reusable splash/hero header component

Displays a prominent article header with:
- Kicker (section label or category)
- Large headline
- Deck (subheading/summary)
- Publication date
- Decorative rule

USAGE EXAMPLE:
<SplashHeader
  kicker="Film Permits"
  headline="Inside the Permits That Built New York City"
  deck="An analysis of decades of film permits reveals the stories Hollywood has told about our city"
  pubDate="2026-03-22"
/>
-->
<script>
  let {
    kicker = '',        // Optional: Section label or category
    headline = '',      // Required: Main headline
    deck = '',          // Optional: Subheading or summary
    pubDate = '',       // Optional: Publication date in YYYY-MM-DD format
  } = $props();

  // Format date to "JANUARY 15, 2024" style
  function formatDate(dateString) {
    if (!dateString) return '';
    
    const [year, month, day] = dateString.split('-').map(Number);
    const date = new Date(year, month - 1, day);
    
    return new Intl.DateTimeFormat('en-US', {
      year: 'numeric',
      month: 'long',
      day: 'numeric',
    }).format(date).toUpperCase();
  }
</script>

<header class="splash-header">
  {#if kicker}
    <div class="kicker">{kicker}</div>
  {/if}

  {#if headline}
    <h1 class="headline">{headline}</h1>
  {/if}

  {#if deck}
    <p class="deck">{deck}</p>
  {/if}

  {#if pubDate}
    <time datetime={pubDate} class="pub-date">{formatDate(pubDate)}</time>
  {/if}
</header>

<style lang="scss">
  @use '../styles' as *;

  .splash-header {
    margin-bottom: var(--spacing-xl);
    text-align: center;
  }

  .kicker {
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: var(--font-weight-bold);
    text-transform: uppercase;
    letter-spacing: var(--letter-spacing-wide);
    color: var(--color-accent);
    margin-bottom: var(--spacing-sm);
  }

  .headline {
    font-family: var(--font-serif);
    font-size: var(--font-size-5xl);
    font-weight: var(--font-weight-bold);
    line-height: var(--leading-heading);
    color: var(--color-dark);
    margin-bottom: var(--spacing-md);
    margin-top: 0;
  }

  .deck {
    font-family: var(--font-serif);
    font-size: var(--font-size-lg);
    line-height: var(--leading-normal);
    color: var(--color-medium-gray);
    margin-bottom: var(--spacing-md);
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
  }

  .pub-date {
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    text-transform: uppercase;
    letter-spacing: var(--letter-spacing-wide);
    color: var(--color-medium-gray);
  }

  /* Decorative rule above the header */
  .splash-header::before {
    content: '';
    display: block;
    width: 100px;
    height: 4px;
    background-color: var(--color-accent);
    margin: 0 auto var(--spacing-md);
  }

  /* Tablet and up: larger headline */
  @include tablet {
    .headline {
      font-size: var(--font-size-6xl);
    }
  }
</style>
