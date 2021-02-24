<template>
  <Layout>
    <AppBanner heading="Performance Marketing" subheading="What I do:">
      <p class="p-sm">
        I am a
        <a
          class="inline-flex border-b-4 border-primary leading-tight"
          href="https://fabrx.co/brightkit/"
          target="_blank"
          rel="noopener noreferrer"
          >Freelance Performance Marketer</a
        >
        with experience in multiple industries. I work with clients to develop actionable marketing campaigns that convert and drive sales.
      </p>
    </AppBanner>
    <section v-if="$page.posts.edges.length" class="mx-auto pt-10">
      <h2 class="font-bold mb-4 text-3xl">Latests Posts</h2>
      <PostList :posts="$page.posts.edges" />
    </section>
    <section v-if="$page.projects.edges.length" class="mx-auto pt-10">
      <h2 class="font-bold mb-4 text-3xl">Latest Project</h2>
      <ProjectList :projects="$page.projects.edges" />
    </section>
  </Layout>
</template>

<page-query>
  query{
    posts: allSanityPost (sortBy: "publishedAt" limit: 3) {
      edges {
        node {
          id
          slug {
            current
          }
          author {
            name
          }
          title
          publishedAt(format: "MMMM D, YYYY")
          mainImage {
            asset {
              id
              localFile(width: 660, quality: 80)
              url
            }
          }
        }
      }
    }
    projects: allSanityProject (sortBy: "completed" limit: 1) {
      edges {
        node {
          id
          slug {
            current
          }
          title
          mainImage {
            asset {
              id
              localFile(width: 1100, quality: 80)
              url
            }
          }
        }
      }
    }
  }
</page-query>

<script>
import AppBanner from '@/components/AppBanner'
import PostList from '@/components/Blog/PostList'
import ProjectList from '@/components/Project/ProjectList'
import AppContact from '@/components/AppContact'

export default {
  components: {
    AppBanner,
    PostList,
    ProjectList,
    AppContact
  },
  metaInfo: {
    title: 'Home',
  },
}
</script>
