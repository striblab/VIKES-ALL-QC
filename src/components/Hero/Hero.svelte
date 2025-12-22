<!--
@component
### Hero component 
Renders a visual replica of the Immersive Template hero. 

#### Optional properties
- sectionLabel: string;
- headline: string;
- timestamp: string;
- heroImageUrl: string;
- heroImageCaption: string;
- heroImageAltText: string;
- dek: string;
- authorName: string;
- authorBioUrl: string;

#### Example
```svelte
<Hero
  sectionLabel = "Section label",
  headline = "Lorem ipsum dolor sit amet consectetur adipiscing elit",
  timestamp = "Dec. 1, 1977",
  heroImageUrl = "https://arc.stimg.co/startribunemedia/4SPNT7DI36ANT2SOB5N5EJAIJU.jpg",
  heroImageCaption = "",
  heroImageAltText = "",
  dek = "Lorem ipsum dolor sit amet consectetur adipiscing elit, fusce sociis at montes vitae tempor enim, venenatis tristique feugiat arcu dis ridiculus.",
  authorName = "Bryan Brussee",
  authorBioUrl = "https://www.startribune.com/bryan-brussee/8455834",
>
```
-->

<script>
  import Grid from "../Grid/Grid.svelte";
  import GridRow from "../Grid/_GridRow.svelte";
  import SectionLabel from "./_SectionLabel.svelte";
  import Headline from "./_Headline.svelte";
  import Timestamp from "./_Timestamp.svelte";
  import Image from "../Image/Image.svelte";
  import Dek from "./_Dek.svelte";
  import Byline from "./_Byline.svelte";

  /** @type {{sectionLabel?: string; headline?: string; timestamp?: string; heroImageUrl?: string; heroImageCaption?: string; heroImageAltText?: string; dek?: string; authorName?: string; authorBioUrl?: string;}} */
  let {
    sectionLabel = "",
    headline = "",
    timestamp = "December 24, 2025 AT 12:01AM",
    heroImageUrl = "",
    heroImageCaption = "",
    heroImageAltText = "",
    dek = "",
    authorName = "Mark Craig",
    authorBioUrl = "https://www.startribune.com/author/mark-craig/6370584",
  } = $props();

  // re-using this function from articlebody because I can't seem to find a place to put it where all components can access the value of headerOffset

  let headerOffset = $state(0);
  function updateCardNavOffset() {
    const header = document.getElementById('global-header');
    if (!header) return;
    headerOffset = header.offsetHeight;
  }
  $effect(() => {
    updateCardNavOffset();
    window.addEventListener('resize', updateCardNavOffset);
    return () => window.removeEventListener('resize', updateCardNavOffset);
  });
</script>

<Grid additionalClasses="">
  <GridRow variant={"fullBleed"}>

    <!-- hero image -->

    <div class="desktop-hero-image hidden lg:block max-w-[1800px] mx-auto" style={`margin-top:${headerOffset}px`}>
      <img class="" alt="Viking Quarter Century Team hero" src="https://ststatic.stimg.co/news/projects/all/2025-VIKES-ALLQC/img/lg-placeholder.png?w=1800" />
    </div>
    <div class="tablet-hero-image hidden md:block lg:hidden max-w-[1800px] mx-auto">
      <img class="" alt="Viking Quarter Century Team hero" src="https://ststatic.stimg.co/news/projects/all/2025-VIKES-ALLQC/img/md-placeholder.png?w=1200" />
    </div>
    <div class="tablet-hero-image block md:hidden max-w-[1800px] mx-auto">
      <img class="" alt="Viking Quarter Century Team hero" src="https://ststatic.stimg.co/news/projects/all/2025-VIKES-ALLQC/img/xs-placeholder.png?w=768" />
    </div>
    <p class="text-center mb-8 rt-Box font-utility-meta-reg-02 text-text-secondary col-span-full ArticleHero_leadart-standard-credit__Y1_wU mt-[6px] px-4">
      Images provided by the Associated Press, photo illustration by Joe Rull
    </p>

    <!-- end hero image -->

  </GridRow>
  
  <GridRow additionalClasses="justify-self-center text-center w-[100vw]">

    <!-- eyebrow -->

    <a role="link" target="_blank" data-testid="link-button" class="Button_button__9QGZa link large-size Button_button-link__auMnb" href="/sports/vikings">
        <p class="px-4 rt-Text break-words text-text-color-01 uppercase font-utility-label-bold-caps-02 text-center">Vikings</p>
    </a>

    <!-- headline -->

    <div class="flex flex-col gap-y-6 md:gap-y-8 text-center max-w-[1200px] mx-auto leading-[1] pb-4 md:pb-6 pt-4">
      <h1 class="font-[publico-headline-black] px-4 text-text-primary text-[1rem] xs:text-[1.8rem] md:text-[3rem] lg:text-[4rem]">Meet the Minnesota <span class="whitespace-nowrap">Star Tribune’s</span> Vikings <span class="whitespace-nowrap">All-Quarter-Century</span> Team</h1>
    </div>

    <!-- dek, byline and timestamp -->

    <div class="flex flex-col gap-y-5 md:justify-items-center md:items-center mx-auto px-4">
      <h2 class="mx-auto font-editorial-non-news-heading-05 text-[.9rem] xs:text-[1.2rem] xs:max-w-[375px] md:text-[1.5rem] md:max-w-[475px] lg:text-[1.75rem] lg:max-w-[800px] text-text-primary">
        Three longtime Vikings reporters picked 27 players and a head coach who were the best at their positions from 2000 to 2025.
      </h2>
      <div class="mt-4">
        <span class="font-utility-label-bold-02 text-text-primary"><a href="https://www.startribune.com/author/mark-craig/6370584" target="_blank" class="whitespace-nowrap">Mark Craig</a></span>, <span class="font-utility-label-bold-02 text-text-primary"><a href="https://www.startribune.com/author/ben-goessling/6134708" target="_blank" class="whitespace-nowrap">Ben Goessling</a></span>, <span class="font-utility-label-bold-02 text-text-primary"><a href="https://www.startribune.com/author/andrew-krammer/6370577" target="_blank" class="whitespace-nowrap">Andrew Krammer</a></span> <span class="text-text-secondary font-utility-label-reg-02 block mt-[6px]">The Minnesota Star Tribune</span>
      </div>
      <span class="mb-4 font-utility-label-reg-caps-03 text-text-secondary mt-0">
        December 24, 2025 AT 12:01AM
      </span>
    </div>
  </GridRow>
  <GridRow additionalClasses="justify-self-center text-center w-[80%] md:w-[60%] mx-auto pt-12 pb-0">
    <hr class="border-[#ffb601] border-[1px]">
    <div class="bg-white w-[60px] relative -mt-[23px] mx-auto px-2">
      <img class="w-[60px] mx-auto" alt="Star Tribune Star" src="https://ststatic.stimg.co/news/projects/all/2025-VIKES-ALLQC/img/strib-star.png?w=120">
    </div>
  </GridRow>
</Grid>