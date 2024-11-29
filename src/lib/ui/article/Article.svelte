<script>
    export let title;
    export let date;
    export let link;
</script>

<article class="article">
    <h2 class="title">{title}</h2>
    <time class="date">{date}</time>
    <div class="description">
        <slot></slot>
    </div>
    <a href={link} class="link">Read more →</a>
</article>

<style>
    .article {
        padding: 1.5rem;
        background: #fff;
        margin-bottom: 1.5rem;
    }

    .title {
        font-size: 1.5rem;
        font-weight: 600;
        margin: 0 0 0.5rem 0;
        color: #1a1a1a;
    }

    .date {
        display: block;
        font-size: 0.875rem;
        color: #666;
        margin-bottom: 1rem;
    }

    .description {
        margin-bottom: 1rem;
        line-height: 1.6;
        color: #333;
    }

    .link {
        display: inline-block;
        color: #2563eb;
        text-decoration: none;
        font-weight: 500;
        transition: color 0.2s;
    }

    .link:hover {
        color: #1d4ed8;
    }
</style>
