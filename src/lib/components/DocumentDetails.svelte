<script>
  export let doc;
</script>

<style>
  .document {
    background-color: white;
    border: 1px solid #999;
    padding: 1rem;
    box-shadow: 2px 2px 6px rgba(0,0,0,0.1);
    margin-bottom: 1rem;
  }

  .document h2 {
    margin-top: 0;
    font-size: 1rem;
  }

  .document p {
    margin: 0.5rem 0;
  }

  .document a {
    color: #0077cc;
    text-decoration: none;
  }

  .document a:hover {
    text-decoration: underline;
  }

  @media (max-width: 1280px) {
    .document {
      width: 90%;
      margin: 0 auto;
    }
  }
</style>

<div class="document">
  <h2>{doc.title}</h2>
  <p><strong>Summary:</strong> {doc.summary}</p>
  <p><a href={doc.url} target="_blank" rel="noopener">Read full document</a></p>
</div>
