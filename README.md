## Next.js Important Note
1. dashbord/(overview)/loading.tsx, page.tsx, apply only in dashbord loading  by using (overview)
2. specific page section load(streaming/loader) : 
    - fallback : pass the loading Component design 
    - Suspense : pass inside of suspense <RevenueChart />
    <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
        <Suspense fallback={<RevenueChartSkeleton />}>
          <RevenueChart />
        </Suspense>
        <LatestInvoices latestInvoices={latestInvoices} />
      </div>
3. i. static rendering is like they dont reflect data instantly 
      - The <SideNav> Component doesn't rely on data and is not personalized to the user, so it can be static.
   ii. dynamic rendering : when data change request in every time of page visit..
    - The components in <Page> rely on data that changes often and will be personalized to the user, so they can be dynamic.
4. Partial Prerendering : 
          i. next.config.js 
              const nextConfig = {
                experimental: {
                  ppr: 'incremental',
                },
              };
          ii. export const experimental_ppr = true; add line code in dashboard layout, and other if needed
          - static + dynamic rendering in same route 
          - increase the performance of application in production mode
          - Suspense to wrap the dynamic parts of your route, Next.js will know which parts of your route are static and which are dynamic.
          
5. Debouncing : its allow to search function of table when user type, it will call after 300 seconds..
        - you can implement own but we use library : pnpm i use-debounce
        - By debouncing, you can reduce the number of requests sent to your database, thus saving resources.
        - FOr Exmaple check ui/search.tsx file..
6. revalidatePath('/dashboard/invoices');
     - re-request from database query and refresh the data..
       

7. Throw Error  : you can use try and cache block to grab the below errors...
    throw new Error('Failed to Delete Invoice');
8. seo tags : 
  import { Metadata } from 'next';
  
  export const metadata: Metadata = {
    title: {
      template: '%s | Acme Dashboard',
      default: 'Acme Dashboard',
    },
    description: 'The official Next.js Learn Dashboard built with App Router.',
    metadataBase: new URL('https://next-learn-dashboard.vercel.sh'),
  };
  // use blelow in every page, it replace the Login text from title template
  export const metadata: Metadata = {
    title: 'Login',
  };