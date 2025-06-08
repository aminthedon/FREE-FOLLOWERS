# FREE-FOLLOWERS
```jsx
import { useState, useEffect } from 'react';

export default function App() {
  const [page, setPage] = useState('home');
  const [username, setUsername] = useState('');
  const [loading, setLoading] = useState(false);
  const [offerCompleted, setOfferCompleted] = useState(false);
  const [countdown, setCountdown] = useState(60);

  // Countdown effect for success page
  useEffect(() => {
    if (offerCompleted && countdown > 0) {
      const timer = setTimeout(() => {
        setCountdown(countdown - 1);
      }, 1000);
      return () => clearTimeout(timer);
    }
  }, [countdown, offerCompleted]);

  const handleClaimClick = (e) => {
    e.preventDefault();
    if (!username.trim()) {
      alert("Please enter your Instagram username!");
      return;
    }
    setPage('offer');
    setLoading(true);
    setTimeout(() => {
      setLoading(false);
    }, 2000); // Simulate loading
  };

  const handleOfferComplete = () => {
    setOfferCompleted(true);
    setPage('success');
  };

  return (
    <div className="bg-white text-gray-800 font-sans">
      {/* Navigation */}
      <header className="p-4 shadow-md bg-gradient-to-r from-purple-500 to-blue-500 text-white fixed top-0 left-0 right-0 z-50">
        <h1 className="text-xl md:text-2xl font-bold text-center">Free Instagram Followers</h1>
      </header>

      {/* Main Content */}
      <main className="pt-20 pb-24 px-4 md:px-8 max-w-3xl mx-auto">
        {page === 'home' && (
          <section className="text-center space-y-6 animate-fadeIn">
            <h2 className="text-3xl md:text-4xl font-extrabold leading-tight">
              Get 100 Free Instagram Followers Instantly!
            </h2>
            <p className="text-lg md:text-xl text-gray-700">
              Just complete one quick offer to unlock your free followers.
            </p>
            <form onSubmit={handleClaimClick} className="space-y-4">
              <input
                type="text"
                placeholder="Enter your Instagram username"
                value={username}
                onChange={(e) => setUsername(e.target.value)}
                className="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
              />
              <button
                type="submit"
                className="w-full py-3 px-6 bg-gradient-to-r from-blue-500 to-purple-600 text-white font-semibold rounded-lg shadow-md hover:from-blue-600 hover:to-purple-700 transition duration-300 transform hover:scale-105"
              >
                Claim Your Followers Now
              </button>
            </form>

            {/* How it works */}
            <div className="mt-8">
              <h3 className="text-xl font-semibold mb-4">How It Works</h3>
              <div className="grid grid-cols-1 sm:grid-cols-3 gap-4">
                <div className="flex flex-col items-center p-4 bg-gray-100 rounded-lg">
                  <span className="text-2xl font-bold text-blue-600 mb-2">1</span>
                  <p className="text-sm text-center">Enter your Instagram username</p>
                </div>
                <div className="flex flex-col items-center p-4 bg-gray-100 rounded-lg">
                  <span className="text-2xl font-bold text-blue-600 mb-2">2</span>
                  <p className="text-sm text-center">Complete a quick offer</p>
                </div>
                <div className="flex flex-col items-center p-4 bg-gray-100 rounded-lg">
                  <span className="text-2xl font-bold text-blue-600 mb-2">3</span>
                  <p className="text-sm text-center">Get 100 free followers instantly</p>
                </div>
              </div>
            </div>

            {/* Trust Badges */}
            <div className="flex justify-center gap-4 mt-6 text-sm text-gray-600">
              <div className="flex items-center gap-2">
                🔒 Secure Process
              </div>
              <div className="flex items-center gap-2">
                🔐 No Password Needed
              </div>
              <div className="flex items-center gap-2">
                ⏱️ Fast Delivery
              </div>
            </div>
          </section>
        )}

        {page === 'offer' && (
          <section className="text-center space-y-6 animate-slideIn">
            {loading ? (
              <>
                <h2 className="text-2xl font-bold">Verifying Account...</h2>
                <div className="w-full h-2 bg-gray-200 rounded-full overflow-hidden">
                  <div className="h-full bg-blue-500 animate-pulse" style={{ width: '60%' }}></div>
                </div>
                <p className="text-gray-600">Connecting to Instagram servers...</p>
              </>
            ) : (
              <>
                <h2 className="text-2xl font-bold">Complete Offer to Unlock Followers</h2>
                <p className="text-gray-600 mb-4">Choose one of the offers below to proceed.</p>

                {/* Simulated CPA Offer Wall */}
                <div className="bg-gray-100 p-4 rounded-lg shadow-inner">
                  <div className="border-b pb-3 mb-3">
                    <h3 className="font-semibold">🔥 Complete 1 Offer</h3>
                    <p className="text-sm text-gray-600">To get 100 Instagram followers</p>
                  </div>
                  <div className="space-y-3">
                    <div className="bg-white p-3 rounded shadow hover:shadow-md cursor-pointer border-l-4 border-blue-500" onClick={handleOfferComplete}>
                      <h4 className="font-medium">Try Premium Dating App</h4>
                      <p className="text-xs text-gray-500">No credit card needed</p>
                    </div>
                    <div className="bg-white p-3 rounded shadow hover:shadow-md cursor-pointer border-l-4 border-purple-500" onClick={handleOfferComplete}>
                      <h4 className="font-medium">Download Fitness App</h4>
                      <p className="text-xs text-gray-500">Available on iOS & Android</p>
                    </div>
                  </div>
                </div>
              </>
            )}
          </section>
        )}

        {page === 'success' && (
          <section className="text-center space-y-6 animate-fadeIn">
            <h2 className="text-3xl font-bold text-green-600">Offer Completed Successfully!</h2>
            <div className="w-full h-3 bg-gray-200 rounded-full overflow-hidden">
              <div className="h-full bg-green-500 animate-progress"></div>
            </div>
            <p className="text-lg">Sending Followers...</p>
            <p className="text-gray-600">Your followers will arrive in 30-60 minutes. Please do not refresh this page.</p>
            
            <div className="mt-6">
              <p className="text-sm text-gray-500">You'll be redirected in {countdown}s</p>
            </div>
          </section>
        )}

        {/* Footer with Legal Links */}
        <footer className="mt-12 text-center text-sm text-gray-500 space-x-4">
          <a href="#terms" className="hover:underline">Terms of Service</a>
          <a href="#privacy" className="hover:underline">Privacy Policy</a>
          <a href="#disclaimer" className="hover:underline">Disclaimer</a>
        </footer>
      </main>

      {/* Floating CTA Button on Mobile */}
      <div className="fixed bottom-4 left-4 right-4 md:hidden">
        {page === 'home' && (
          <button
            onClick={handleClaimClick}
            className="w-full py-3 bg-gradient-to-r from-blue-500 to-purple-600 text-white font-semibold rounded-lg shadow-lg hover:from-blue-600 hover:to-purple-700 transition duration-300"
          >
            Claim Followers Now
          </button>
        )}
      </div>

      {/* Google Analytics and Facebook Pixel Scripts */}
      <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
      <script dangerouslySetInnerHTML={{
        __html: `
          window.dataLayer = window.dataLayer || [];
          function gtag(){dataLayer.push(arguments);}
          gtag('js', new Date());
          gtag('config', 'GA_MEASUREMENT_ID');
        `,
      }} />

      <script dangerouslySetInnerHTML={{
        __html: `
          !function(f,b,e,v,n,t,s)
          {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
          n.callMethod.apply(n,arguments):n.queue.push(arguments)};
          if(!f._fbq)f._fbq=n;t=b.createElement(e);t.async=!0;
          t.src=v;s=b.getElementsByTagName(e)[0];
          s.parentNode.insertBefore(t,s)}(window, document,'script',
          'https://connect.facebook.net/en_US/fbevents.js');
          fbq('init', 'FACEBOOK_PIXEL_ID');
          fbq('track', 'PageView');
        `,
      }} />

      {/* Meta Tags for Sharing */}
      <meta property="og:title" content="Get 100 Free Instagram Followers Instantly!" />
      <meta property="og:description" content="Just complete one quick offer to unlock your free Instagram followers." />
      <meta property="og:image" content="https://placehold.co/600x400?text=Free+Instagram+Followers" />
      <meta property="og:url" content="https://yourwebsite.com" />
      <meta name="twitter:card" content="summary_large_image" />

      <style jsx>{`
        @keyframes fadeIn {
          from { opacity: 0; }
          to { opacity: 1; }
        }
        @keyframes slideIn {
          from { transform: translateY(20px); opacity: 0; }
          to { transform: translateY(0); opacity: 1; }
        }
        @keyframes progressAnimation {
          from { width: 0%; }
          to { width: 100%; }
        }
        .animate-fadeIn {
          animation: fadeIn 0.6s ease-out forwards;
        }
        .animate-slideIn {
          animation: slideIn 0.6s ease-out forwards;
        }
        .animate-progress {
          animation: progressAnimation 3s linear forwards;
        }
      `}</style>
    </div>
  );
}
```
