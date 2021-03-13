<script lang="typescript">
  import { onMount } from 'svelte'
  import { gsap, Expo } from 'gsap'
  import { ScrollTrigger } from 'gsap/ScrollTrigger'

  gsap.registerPlugin(ScrollTrigger)

  let count: number = 0
  onMount(() => {
    const interval = setInterval(() => count++, 1000)
    return () => {
      clearInterval(interval)
    }
  })

  onMount(() => {
    gsap.to('.face-section', {
      scrollTrigger: {
        trigger: '.face-section',
        toggleActions: 'restart none restart none',
        start: 'top top',
        end: 'bottom top',
        scrub: true,
      },
      opacity: 0,
    })

    const faceTl = gsap.timeline({
      scrollTrigger: '.face-section',
    })

    faceTl.to('.title-text', {
      y: '0%',
      stagger: 0.12,
      duration: 2,
      ease: Expo.easeInOut,
      delay: -0.5,
    })
    faceTl.to('.manifesto', {
      opacity: 1,
      duration: 1,
      delay: -0.5,
    })
    faceTl.to('.logo', {
      opacity: 1,
      duration: 1,
      delay: -0.5,
    })
  })
</script>

<div class="woowahan-fonts">
  <div class="base-column">
    <section class="section face-section">
      <div class="face-container">
        <h1 class="title">
          <span class="title-text-mask">
            <span class="title-text">모두에게</span>
          </span>
          <span class="title-text-mask">
            <span class="title-text">&nbsp;친숙하고,</span>
          </span>
          <br />
          <span class="title-text-mask">
            <span class="title-text">모두에게</span>
          </span>
          <span class="title-text-mask">
            <span class="title-text">&nbsp;사랑받는</span>
          </span>
          <br />
          <span class="title-text-mask">
            <span class="title-text">바로</span>
          </span>
          <span class="title-text-mask">
            <span class="title-text">&nbsp;그 글씨체.</span>
          </span>
        </h1>
        <p class="manifesto">
          우아한형제들은 누구나 제약 없이
          <br />
          아름다운 한글을 쓸 수 있도록
          <br />
          배달의민족 글꼴을 만들어
          <br />
          무료로 배포하고 있습니다.
        </p>
        <img
          class="logo"
          src="/images/woowabros-logo.png"
          alt="우아한형제들 로고"
        />
      </div>
    </section>
  </div>

  <section class="section bm-euljiro">
    <div class="base-column">
      <h2 class="font-name">배달의민족 한나는열한살체</h2>
      <p class="font-description">
        배달의민족 한나체는 아크릴 판 위에 시트지를 붙여 칼로 잘라낸 1960~70년대
        간판을 모티브로 만들어 삐뚤빼뚤 조형성이 떨어지는 듯한 느낌의
        서체입니다. 초기 한나체의 균일하지 못했던 글자 사이의 공간을 수정하여
        더욱 완성도 있는 글씨체인 ‘한나는열한살’체로 거듭났습니다.
      </p>
    </div>

    <div class="images-container">
      <div class="font-image-wrapper">
        <img
          class="font-image"
          src="/images/font-animation-hanna1.jpg"
          alt="폰트 이미지"
        />
      </div>
      <div class="font-image-wrapper">
        <img
          class="font-image"
          src="/images/font-animation-hanna2.jpg"
          alt="폰트 이미지"
        />
      </div>
      <div class="font-image-wrapper">
        <img
          class="font-image"
          src="/images/font-animation-hanna3.jpg"
          alt="폰트 이미지"
        />
      </div>
      <div class="font-image-wrapper">
        <img
          class="font-image"
          src="/images/font-animation-hanna4.jpg"
          alt="폰트 이미지"
        />
      </div>
      <div class="font-image-wrapper">
        <img
          class="font-image"
          src="/images/font-animation-hanna5.jpg"
          alt="폰트 이미지"
        />
      </div>
    </div>
  </section>
</div>

<style>
  :global(html, body) {
    height: 100%;
  }

  .woowahan-fonts {
    height: 100%;
  }

  .base-column {
    width: calc(100% - 2.5rem);
    margin: 0 auto;
    max-width: 40rem;
    height: 100%;
  }

  .section {
    min-height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 3rem 0;
  }

  .logo {
    width: 2.2rem;
    height: auto;
    margin-top: 1rem;
    opacity: 0;
  }

  .title {
    font-size: 0;
    width: 100%;
    line-height: 1;
  }

  .title-text-mask {
    overflow: hidden;
    line-height: 1;
    height: 2.3rem;
  }

  .title-text-mask:not(:first-child) {
    margin-top: 0.6rem;
  }

  .title-text {
    font-size: 2.3rem;
    transform: translateY(150%);
    will-change: transform;
    line-height: 1;
    height: 1em;
  }

  .manifesto {
    font-size: 1.3rem;
    line-height: 1.3;
    color: var(--bm-gray);
    margin-top: 1rem;
    opacity: 0;
  }

  .font-name {
    font-size: 2rem;
    line-height: 1.2;
  }

  .font-description {
    line-height: 1.4;
    color: var(--bm-gray);
    font-size: 1.1rem;
    margin-top: 1rem;
  }

  .images-container {
    overflow-x: auto;
    white-space: nowrap;
    margin-top: 1.5rem;
    font-size: 0;
  }

  .images-container::-webkit-scrollbar {
    display: none;
  }

  .font-image-wrapper {
    border-radius: 0.6rem;
    overflow: hidden;
    position: relative;
    width: 50%;
    display: inline-block;
  }

  .font-image-wrapper::before {
    content: '';
    display: block;
    padding-bottom: 73%;
  }

  .font-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    position: absolute;
    top: 0;
    left: 0;
  }
</style>
