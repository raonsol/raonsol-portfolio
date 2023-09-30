# raonsol-portfolio

> `nextjs-notion-starter-kit`을 기반으로 제작된 포트폴리오 웹사이트

## Intro

본 웹사이트는 Notion을 CMS로 사용하고, [react-notion-x](https://github.com/NotionX/react-notion-x), [Next.js](https://nextjs.org/)를 사용하여 정적 웹사이트로 변환합니다.

## Features

- 번거로운 세팅 불필요 ([단일 config 파일](./site.config.ts)) 💪
- [react-notion-x](https://github.com/NotionX/react-notion-x)를 사용한 Notion 연동 지원
- Next.js, TS, React 사용
- 페이지 로딩 속도 최적화
- 부드러운 이미지 프리뷰
- 공유용 OG 이미지 생성 자동화
- 직관적인 URL 생성 자동화
- ToC(목차) 자동 생성
- 다크모드 지원
- CMD+K / CMD+P 단축키로 검색 지원
- 반응형 웹 지원
- Next.js와 Vercel 지원

## Setup

**모든 환경설정은 [site.config.ts](./site.config.ts)에 정의되어 있습니다.**

Node.js 최신버전을 권장합니다. (16버전 이상).

1. Fork / clone
2. [site.config.ts](./site.config.ts)에서 환경설정 변경
3. `npm install`
4. `npm run dev` (개발서버로 테스트)
5. `npm run deploy` (Vercel로 배포, 선택사항)

변경해주어야 할 중요한 환경설정은 `rootNotionPageId`입니다.

웹사이트로 변환할 Notion root 페이지가 **전체 공개** 상태인지 확인하고 링크를 복사합니다. 그 후 Notion ID(URL에서 마지막의 `7875426197cf461698809def95960ebf`형태로 생긴 값)을 추출합니다.

Notion workspace ID(선택사항)을 찾기 위해서는 개발자 도구를 사용해야 합니다. 원하는 Notion 페이지에서 개발자 도구를 열고 `block.space_id`를 입력하면 Notion workspace ID를 확인할 수 있습니다.

## URL Paths

개발서버에서 구동할 때와 운영서버에서 구동할 때의 URL이 다릅니다. 개발서버에서는 `/nextjs-notion-blog-d1b5dcf8b9ff425b8aef5ce6f0730202`와 같은 형태로 URL이 생성되지만, 운영서버에서는 `/nextjs-notion-blog`와 같은 형태로 URL이 생성됩니다.

기본적인 slug 생성 규칙은 변경이 가능합니다. DB에 `Slug` 프로퍼티를 추가하면 해당 프로퍼티를 URL로 사용합니다.

> 중요: 만약 워크스페이스에 동일한 slug를 가진 페이지가 여러개 있다면, 에러가 발생합니다.

## Preview Images

<p align="center">
  <img alt="Example preview image" src="https://user-images.githubusercontent.com/552829/160142320-35343317-aa9e-4710-bcf7-67e5cdec586d.gif" width="458">
</p>

[next/image](https://nextjs.org/docs/api-reference/next/image)를 사용해서 Lazy loading을 지원합니다. 이 패키지는 [lqip-modern](https://github.com/transitive-bullshit/lqip-modern)을 사용해서 LQIP 프리뷰 이미지를 생성하므로써 부드러운 로딩 화면을 보여주게 됩니다.

프리뷰 이미지는 **기본적으로 활성화**되어 있습지만, 생성하는 데 시간이 오래 걸릴 수 있습니다. 만약 끄고 싶다면 `site.config.ts`에서 `isPreviewImageSupportEnabled`를 `false`로 설정하면 됩니다.

## Styles

모든 CSS 스타일은 [styles/global.css](./styles/global.css)에 정의되어 있습니다. 이 CSS 파일로 Notion에서 가져온 요소들의 스타일을 지정하게 됩니다.

모든 Notion 블록은 각각 고유한 클래스명을 가지고 있습니다. 따라서 다음과 같이 각 블록을 선택할 수 있습니다.

```css
.notion-block-260baa77f1e1428b97fb14ac99c7c385 {
  display: none;
}
```

## Dark Mode

<p align="center">
  <img alt="Light Mode" src="https://transitive-bs.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F83ea9f0f-4761-4c0b-b53e-1913627975fc%2Ftransitivebullsh.it_-opt.jpg?table=block&id=ed7e8f60-c6d1-449e-840b-5c7762505c44&spaceId=fde5ac74-eea3-4527-8f00-4482710e1af3&width=2000&userId=&cache=v2" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Dark Mode" src="https://transitive-bs.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc0839d6c-7141-48df-8afd-69b27fed84aa%2Ftransitivebullsh.it__(1)-opt.jpg?table=block&id=23b11fe5-d6df-422d-9674-39cf7f547523&spaceId=fde5ac74-eea3-4527-8f00-4482710e1af3&width=2000&userId=&cache=v2" width="45%">
</p>

다크모드 전환은 footer의 아이콘을 클릭하면 됩니다.

## Automatic Social Images

<p align="center">
  <img alt="Example social image" src="https://user-images.githubusercontent.com/552829/162001133-34d4cf24-123a-4569-a540-f683b22830d1.jpeg" width="600">
</p>

SNS 공유용 OG 이미지는 Notion 페이지의 내용을 기반으로 자동으로 생성됩니다.

 [Vercel OG Image Generation](https://vercel.com/docs/concepts/functions/edge-functions/og-image-generation)을 사용하여 자동으로 생성되며, [api/social-images.tsx](./pages/api/social-image.tsx)을 수정해서 스타일을 변경할 수 있습니다.

## Automatic Table of Contents

<p align="center">
  <img alt="Smooth ToC Scrollspy" src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcb2df62d-9028-440b-964b-117711450921%2Ftoc2.gif?table=block&id=d7e9951b-289c-4ff2-8b82-b0a61fe260b1&cache=v2" width="240">
</p>

기본적으로 모든 페이지의 목차는 `aside`에 표시됩니다. 스크롤에 따라 자동으로 현재 위치를 표시해주며, 클릭할 시 해당 위치로 이동합니다.

만약 페이지에 목차 항목이 `minTableOfContentsItems` (기본 3) 값 미만이라면, 목차는 표시되지 않습니다. 또한 인덱스 페이지와 브라우저 창이 너무 작을 경우에도 표시되지 않습니다.

이 목차는 Notion에서 사용하는 목차 블록과 같은 로직을 사용합니다. (자세한 내용은 [getPageTableOfContents](https://github.com/NotionX/react-notion-x/blob/master/packages/notion-utils/src/get-page-table-of-contents.ts) 참고 바랍니다.

## Responsive

<p align="center">
  <img alt="Mobile article page" src="https://user-images.githubusercontent.com/552829/160132983-c2dd5830-80b3-4a0e-a8f1-abab5dbeed11.jpg" width="300">
</p>

모든 페이지는 반응형으로 제작되었습니다. 모바일 환경에서도 최적화된 UI를 제공합니다.
