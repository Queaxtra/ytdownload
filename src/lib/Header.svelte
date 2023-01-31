<script lang="ts">
    let url = "";
    let searchingSong = false;
    let searchDataName: any;
    let searchDataDownloadMP3: any;
    let searchDataSize: any;

    async function searchSong() {
        searchingSong = true;
        await fetch(`https://ytdownloader.projectsrpp.repl.co/?q=${url}`).then((res) => res.json()).then((data) => {
            searchDataName = data.title;
            searchDataDownloadMP3 = data.download[0];
            searchDataSize = data.download[0];
        }).then(() => {
            searchingSong = false;
        })
    }
</script>


<div class="text-center">
    <h2 class="text-5xl font-semibold text-white/80 relative mt-60 transition-all duration-300">YTDownload</h2>
    <p class="text-lg relative mt-3 italic text-white/50 transition-all duration-300">No ADS, Unlimited Download</p>

    <div class="relative mt-5">
        <input bind:value={url} class="transition-all duration-300 py-2 bg-[#262626] border-2 border-[#404040] rounded w-80 px-5 text-white/70" type="url" placeholder="Enter a Youtube URL.">
        {#if !url}
        <button disabled class="transition-all duration-300 opacity-50 my-3 md:my-0 lg:my-0 mx-3 py-2 px-5 bg-[#262626] border-2 border-[#404040] rounded text-white/70"><i class="fa-sharp fa-solid fa-magnifying-glass"></i> Search</button>
        {:else}
        {#if searchingSong === true}
        <button on:click={searchSong} class="transition-all duration-300 my-3 md:my-0 lg:my-0 mx-3 py-2 px-5 bg-[#262626] border-2 border-[#404040] rounded text-white/70"><i class="fa-solid fa-rotate animate-spin"></i> Searching</button>
        {:else}
        <button on:click={searchSong} class="transition-all duration-300 my-3 md:my-0 lg:my-0 mx-3 py-2 px-5 bg-[#262626] border-2 border-[#404040] rounded text-white/70"><i class="fa-sharp fa-solid fa-magnifying-glass"></i> Search</button>
        {/if}
        {/if}
    </div>

    {#if searchDataName}
    <div class="bg-[#262626] p-5 rounded drop-shadow-md w-80 relative ml-auto mr-auto left-0 right-0 mt-10">
        <p class="relative text-white/70 my-4">{searchDataName}</p>
        <a href="{searchDataDownloadMP3.ul}" class="transition-all duration-300 relative md:my-0 lg:my-0 mx-3 py-2 px-5 bg-[#262626] border-2 border-[#404040] rounded text-white/70"><i class="fa-solid fa-download"></i> Download ({searchDataSize.size})</a>
    </div>
    {/if}
</div>