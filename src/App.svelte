<script lang="typescript">
  import { onMount } from 'svelte'
  import { gsap, Expo, Power4 } from 'gsap'
  import { ScrollTrigger } from 'gsap/ScrollTrigger'
  import { squirclify } from 'squircle.js'
  import { hannaProPreview } from './hanna-pro-preview'

  gsap.registerPlugin(ScrollTrigger)

  let count: number = 0
  onMount(() => {
    const interval = setInterval(() => count++, 1000)
    return () => {
      clearInterval(interval)
    }
  })

  let proAnimationTimeout: number[] = []

  function playProPreviewAnimation() {
    const preview = document.querySelector(
      '.hanna-pro-preview'
    ) as HTMLTextAreaElement

    for (const timeout of proAnimationTimeout) {
      window.clearTimeout(timeout)
    }

    proAnimationTimeout = []

    hannaProPreview.forEach((split, i) => {
      const timeout = window.setTimeout(() => {
        preview.value = split

        if (i === hannaProPreview.length - 1) {
          const timeout = window.setTimeout(() => {
            preview.value =
              hannaProPreview[hannaProPreview.length - 1] +
              '\n이 곳에 직접 입력해보세요!'
          }, 300)

          proAnimationTimeout.push(timeout)
        }
      }, i * 50)

      proAnimationTimeout.push(timeout)
    })
  }

  // Apply squircle
  onMount(() => {
    const downloadBtns = document.querySelectorAll('.download-btn')
    squirclify(Array.from(downloadBtns) as HTMLElement[])
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
      y: '30vh',
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

    gsap.to('.bmhanna-11yrs-section .images-container', {
      scrollTrigger: {
        trigger: '.bmhanna-11yrs-section .images-container',
        start: 'top bottom',
        end: 'bottom top',
        scrub: 0.5,
      },
      x: '-80rem',
    })

    gsap.to('.bmeuljiro-section .images-container', {
      scrollTrigger: {
        trigger: '.bmeuljiro-section .images-container',
        start: 'top bottom',
        end: 'bottom top',
        scrub: 0.5,
      },
      x: '-80rem',
    })

    gsap.to('.bmhanna-pro-section', {
      scrollTrigger: {
        trigger: '.bmhanna-pro-section .font-name',
        start: 'top 80%',
        onEnter: () => {
          document.body.classList.add('dark')
        },
        onLeaveBack: () => {
          document.body.classList.remove('dark')
        },
      },
    })

    gsap.to('.bmhanna-pro-section', {
      scrollTrigger: {
        trigger: '.bmhanna-pro-section',
        start: 'bottom 80%',
        onEnter: () => {
          document.body.classList.remove('dark')
        },
        onLeave: () => {
          console.log('leave')
        },
        onEnterBack: () => {
          console.log('enter back')
        },
        onLeaveBack: () => {
          document.body.classList.add('dark')
        },
      },
    })

    gsap.to('.hanna-pro-preview', {
      scrollTrigger: {
        trigger: '.hanna-pro-preview',
        start: 'top 80%',
        onEnter: () => {
          playProPreviewAnimation()
        },
      },
    })
  })
</script>

<div class="woowahan-fonts">
  <div class="base-column">
    <section class="section face-section">
      <div class="face-container">
        <img
          class="font-title"
          src="/images/font-title.png"
          alt="폰트 타이틀"
        />
        <h1 class="title hanna">
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
        <p class="manifesto hanna">
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

  <section class="section bmhanna-11yrs-section">
    <div class="base-column">
      <span class="font-birthday">2012, 1st</span>
      <h2 class="font-name hanna">배달의민족 한나는열한살체</h2>
      <p class="font-description">
        배달의민족 한나체는 아크릴 판 위에 시트지를 붙여 칼로 잘라낸 1960~70년대
        간판을 모티브로 만들어 삐뚤빼뚤 조형성이 떨어지는 듯한 느낌의
        서체입니다. 초기 한나체의 균일하지 못했던 글자 사이의 공간을 수정하여
        더욱 완성도 있는 글씨체인 ‘한나는열한살’체로 거듭났습니다.
      </p>
    </div>

    <div class="images-container-guidance">
      <div class="font-image-dummy" />
      <div class="images-container">
        {#each Array(5) as _, i}
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
        {/each}
      </div>
      <div class="font-image-dummy" />
    </div>

    <div class="base-column">
      <div class="downloads-container">
        <a
          class="download-btn-link"
          download
          href="https://d1mphx2csg3pcg.cloudfront.net/fonts/BMHANNA_11yrs_ttf.ttf"
        >
          <button class="download-btn">Windows용 다운로드 (TTF)</button>
        </a>
        <a
          class="download-btn-link"
          download
          href="https://d1mphx2csg3pcg.cloudfront.net/fonts/BMHANNA_11yrs_otf.otf"
        >
          <button class="download-btn">Mac용 다운로드 (OTF)</button>
        </a>
      </div>
    </div>
  </section>

  <section class="section bmhanna-pro-section">
    <div class="base-column">
      <span class="font-birthday">2018, 7th</span>
      <h2 class="font-name hanna">배달의민족 한나체 Pro</h2>
      <p class="font-description">
        배달의민족 한나체 Pro는 맛있는 음식 이미지가 구석구석 숨어있는
        서체입니다. 한글 조합은 되지만 실제로는 잘 쓰이지 않는 글자를 음식
        이미지로 대체하여 타이핑할 때 뜬금없이 음식 그림이 뿅! 나왔다
        사라집니다. 배고플 때 쓰면 더 배고파지는 것이 특징입니다.
      </p>
      <textarea class="hanna-pro-preview hanna-pro" />
      <button class="replay-pro-animation" on:click={playProPreviewAnimation}>
        <span class="icon f7-icons">arrow_counterclockwise</span>
        다시 재생
      </button>

      <div class="downloads-container">
        <a
          class="download-btn-link"
          download
          href="https://d1mphx2csg3pcg.cloudfront.net/fonts/BMHANNAPro.ttf"
        >
          <button class="download-btn">Windows용 다운로드 (TTF)</button>
        </a>
        <a
          class="download-btn-link"
          download
          href="https://d1mphx2csg3pcg.cloudfront.net/fonts/BMHANNAProOTF.otf"
        >
          <button class="download-btn">Mac용 다운로드 (OTF)</button>
        </a>
      </div>
    </div>
  </section>

  <section class="section bmeuljiro-section">
    <div class="base-column">
      <span class="font-birthday">2019,8th</span>
      <h2 class="font-name euljiro">배달의민족 을지로체</h2>
      <p class="font-description">
        배달의민족 을지로체는 무명의 간판 글씨 장인이 그린 을지로 일대 가게들의
        간판을 바탕으로 만든 것입니다. 획 마다의 힘찬 시작과 페인트 붓의
        여유로운 끝 모양이 특징입니다.
      </p>
    </div>

    <div class="images-container-guidance">
      <div class="font-image-dummy" />
      <div class="images-container">
        {#each Array(5) as _, i}
          <div class="font-image-wrapper">
            <img
              class="font-image"
              src="/images/font-euljiro1.jpg"
              alt="폰트 이미지"
            />
          </div>
          <div class="font-image-wrapper">
            <img
              class="font-image"
              src="/images/font-euljiro2.jpg"
              alt="폰트 이미지"
            />
          </div>
          <div class="font-image-wrapper">
            <img
              class="font-image"
              src="/images/font-euljiro3.jpg"
              alt="폰트 이미지"
            />
          </div>
          <div class="font-image-wrapper">
            <img
              class="font-image"
              src="/images/font-euljiro4.jpg"
              alt="폰트 이미지"
            />
          </div>
          <div class="font-image-wrapper">
            <img
              class="font-image"
              src="/images/font-euljiro5.jpg"
              alt="폰트 이미지"
            />
          </div>
          <div class="font-image-wrapper">
            <img
              class="font-image"
              src="/images/font-euljiro6.jpg"
              alt="폰트 이미지"
            />
          </div>
        {/each}
      </div>
      <div class="font-image-dummy" />
    </div>

    <div class="base-column">
      <div class="downloads-container">
        <a
          class="download-btn-link"
          download
          href="https://d1mphx2csg3pcg.cloudfront.net/fonts/BMEULJIROTTF.ttf"
        >
          <button class="download-btn">Windows용 다운로드 (TTF)</button>
        </a>
        <a
          class="download-btn-link"
          download
          href="https://d1mphx2csg3pcg.cloudfront.net/fonts/BMEULJIRO.otf"
        >
          <button class="download-btn">Mac용 다운로드 (OTF)</button>
        </a>
      </div>
    </div>
  </section>
</div>

<style lang="scss">
  :global(html, body) {
    width: 100%;
    overflow-x: hidden;
  }

  :global(body) {
    transition: background-color 500ms ease, color 500ms ease;
  }

  :global(body) {
    &.dark {
      background-color: #000;
      color: #f8f8f8;
    }
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
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 3rem 0 6rem;
    will-change: transform;
    position: relative;
  }

  .logo {
    width: 2.2rem;
    height: auto;
    margin-top: 1rem;
    opacity: 0;
  }

  .face-section {
    align-items: flex-end;

    .font-title {
      position: absolute;
      top: 50%;
      left: 0;
      transform: translateY(-50%);
      width: 60%;
      z-index: -1;
    }

    .face-container {
      text-align: right;
    }
  }

  @media only screen and (max-width: 850px) {
    .face-section {
      align-items: flex-start;

      .font-title {
        position: static;
        width: 100%;
        max-width: 20rem;
        transform: none;
      }

      .face-container {
        text-align: left;
      }
    }
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

  .font-birthday {
    font-size: 0.8rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
  }

  .font-name {
    font-size: 2rem;
    line-height: 1.2;
  }

  .font-description {
    line-height: 1.4;
    color: var(--bm-gray);
    font-size: 1.1rem;
    font-weight: 500;
    margin-top: 0.7rem;
  }

  .images-container-guidance {
    margin-top: 2rem;
    white-space: nowrap;
    font-size: 0;
  }

  .images-container {
    display: inline-block;
    white-space: nowrap;
    font-size: 0;
    will-change: transform;
  }

  .images-container::-webkit-scrollbar {
    display: none;
  }

  .font-image-wrapper {
    border-radius: 0.6rem;
    overflow: hidden;
    position: relative;
    width: 15rem;
    display: inline-block;
  }

  .font-image-wrapper:not(:first-child) {
    margin-left: 1rem;
  }

  .font-image-wrapper::before {
    content: '';
    display: block;
    padding-bottom: 73%;
  }

  .font-image-dummy {
    display: inline-block;
    width: max(1.25rem, calc(50% - 20rem));
  }

  .font-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    position: absolute;
    top: 0;
    left: 0;
  }

  .downloads-container {
    margin-top: 2.5rem;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;

    .download-btn-link {
      &:not(:first-child) {
        margin: 0 0 0 0.5rem;
      }
    }

    .download-btn {
      flex: 1;
      max-width: 11rem;
      cursor: pointer;
      appearance: none;
      border: none;
      background: none;
      outline: none;
      background-color: #000;
      color: #fff;
      padding: 1rem;
      border-radius: 0.7rem;
      font-size: 0.7rem;
      font-weight: 600;
      white-space: nowrap;
      transition: background-color 500ms ease, color 500ms ease;

      @media only screen and (max-width: 450px) {
        min-width: 100%;

        &:not(:first-child) {
          margin: 0.5rem 0 0 0;
        }
      }
    }
  }

  :global(body.dark) {
    .download-btn {
      color: var(--bm-bright);
      background-color: var(--bm-dark-gray);
    }
  }

  .hanna-pro-preview {
    margin-top: 1.5rem;
    background-color: #e8e8e8;
    border: none;
    display: block;
    width: 100%;
    border-radius: 15px;
    height: 17rem;
    resize: none;
    outline: none;
    padding: 1rem;
    font-size: 1.5rem;
    line-height: 1.5;
    transition: background-color 500ms ease, color 500ms ease;
  }

  :global(body.dark) {
    .hanna-pro-preview {
      background-color: var(--bm-dark-gray);
      color: var(--bm-bright);
    }
  }

  .replay-pro-animation {
    display: flex;
    align-items: center;
    appearance: none;
    border: none;
    background: none;
    color: var(--bm-bright);
    text-align: center;
    font-size: 0.8rem;
    margin-left: auto;
    margin-top: 0.7rem;
    outline: none;
    cursor: pointer;

    .icon {
      margin-right: 0.3rem;
      position: relative;
      top: -0.05rem;
    }
  }
</style>
