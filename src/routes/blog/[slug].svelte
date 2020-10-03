<script context="module">
    export async function preload({ params, query }) {
        // the `slug` parameter is available because
        // this file is called [slug].html
        const res = await this.fetch(`blog/${params.slug}.json`);
        const data = await res.json();

        if (res.status === 200) {
            return { post: data };
        } else {
            this.error(res.status, data.message);
        }
    }
</script>

<script lang="ts">
    export let post;
</script>

<header>
    <p>{post.printReadingTime}</p>
    <h1>{post.title}</h1>
    <hr />
</header>

<div>
    <article>
        {@html post.html}
    </article>
    <hr />
</div>
