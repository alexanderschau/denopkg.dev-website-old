<script>
  let registry = "";
  let tag = "";
  let path = "";
  let repoPath = "";
  $: repoPath = getRepoData(registry);
  const checkGitHub = /github\.com\/(.*?)\/((?:(?!\.git).)*)/;
  const checkGitLab = /gitlab\.com\/(.*?)\/((?:(?!\.git).)*)/;
  const getRepoData = (url) => {
    const checkGh = url.match(checkGitHub);
    if (checkGh) {
      return `gh/${checkGh[1]}/${checkGh[2]}`;
    }
    const checkGl = url.match(checkGitLab);
    if (checkGl) {
      return `gl/${checkGl[1]}/${checkGl[2]}`;
    }
  };
</script>

<div
  class="absolute top-0 left-0 h-full w-full text-center bg-secondary dark:bg-secondary-dark text-primary dark:text-primary-dark"
>
  <div class="max-w-xl mx-auto my-10 px-2">
    <svg
      class="mx-auto fill-current"
      width="4rem"
      height="4rem"
      viewBox="0 0 64 64"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path d="M0 6V0H64V6H0Z" />
      <path
        fill-rule="evenodd"
        clip-rule="evenodd"
        d="M0 10V64H64V10H0ZM48 16V48H32V16H48Z"
      />
    </svg>

    <div class="font-bold text-3xl my-5">Deno Package Registry</div>
    <div class="flex">
      <input
        bind:value={registry}
        type="text"
        placeholder="Repository URL"
        class="input flex-14"
      />
      <div class="my-auto mx-3">@</div>
      <input
        bind:value={tag}
        type="text"
        placeholder="Tag Name"
        class="input flex-5"
      />
    </div>
    <input
      bind:value={path}
      type="text"
      placeholder="File Path (default: /mod.ts)"
      class="input flex-5"
    />
    {#if repoPath}
      <div
        class="py-3 px-4 text-left rounded-lg bg-primary bg-opacity-2 dark:bg-primary-dark dark:bg-opacity-2"
      >
        Your can access your package under:
        <div class="font-bold break-words">
          https://denopkg.dev/{repoPath}{tag != "" ? "@" + tag : ""}{path !=
            "" && path[0] != "/"
            ? "/" + path
            : path}
        </div>
      </div>
    {/if}
    <div class="italic opacity-30 my-3">
      made by <a class="underline" target="_blank" href="https://alexander.sbs"
        >@alexanderschau</a
      > | <a class="underline" target="_blank" href="https://github.com/alexanderschau/denopkg.dev"
      >GitHub repo</a>
    </div>
  </div>
</div>
