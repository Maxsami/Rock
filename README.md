#import React, { useState, useEffect } from 'react';
import { 
  Menu, X, MapPin, Phone, Mail, Star, 
  Coffee, Wifi, Users, BedDouble, 
  ChefHat, ArrowRight, ChevronLeft, ChevronRight, PhoneCall, 
  Download, FileText, CheckCircle, ShieldCheck
} from 'lucide-react';

const App = () => {
  const [isScrolled, setIsScrolled] = useState(false);
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [showServicesContent, setShowServicesContent] = useState(false);
  const [roomCategory, setRoomCategory] = useState('luxury');
  const [currentSlide, setCurrentSlide] = useState(0);

  // Handle scroll for sticky navbar
  useEffect(() => {
    const handleScroll = () => {
      setIsScrolled(window.scrollY > 50);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  // Slider Data
  const gallerySlides = [
    {
      image: "https://images.unsplash.com/photo-1519167758481-83f550bb49b3?ixlib=rb-1.2.1&auto=format&fit=crop&w=1200&q=80",
      title: "Grand Banquet Hall",
      subtitle: "Where memories are made"
    },
    {
      image: "https://images.unsplash.com/photo-1550966871-3ed3c47e2ce2?ixlib=rb-1.2.1&auto=format&fit=crop&w=1200&q=80",
      title: "Gokul Raj Dining",
      subtitle: "A taste of elegance"
    },
    {
      image: "https://images.unsplash.com/photo-1611892440504-42a792e24d32?ixlib=rb-1.2.1&auto=format&fit=crop&w=1200&q=80",
      title: "Royal Comfort",
      subtitle: "Rest like a king"
    }
  ];

  // Auto-slide logic
  useEffect(() => {
    const slideInterval = setInterval(() => {
      setCurrentSlide((prev) => (prev + 1) % gallerySlides.length);
    }, 4000);
    return () => clearInterval(slideInterval);
  }, []);

  const nextSlide = () => setCurrentSlide((prev) => (prev + 1) % gallerySlides.length);
  const prevSlide = () => setCurrentSlide((prev) => (prev - 1 + gallerySlides.length) % gallerySlides.length);

  // Rooms Data with "Badges" for AI/UX optimization
  const luxuryRooms = [
    { id: 1, name: "Premium Suite", price: "Rs. 5000", img: "https://images.unsplash.com/photo-1590490360182-c33d57733427?w=800&q=80", desc: "King size bed, city view, 80 sqft spacious area.", badge: "Best Seller" },
    { id: 2, name: "Deluxe Executive", price: "Rs. 3500", img: "https://images.unsplash.com/photo-1560448204-e02f11c3d0e2?w=800&q=80", desc: "Modern amenities for business travelers.", badge: "Top Value" },
    { id: 3, name: "Standard Luxury", price: "Rs. 2500", img: "https://images.unsplash.com/photo-1566665797739-1674de7a421a?w=800&q=80", desc: "Comfortable stay with all basic luxury needs.", badge: null },
  ];

  const familyRooms = [
    { id: 101, name: "Grand Family Suite", price: "Rs. 6000", img: "https://images.unsplash.com/photo-1596436889106-be35e843f974?w=800&q=80", desc: "Two connecting rooms with large living space.", badge: "Families Love This" },
    { id: 102, name: "Quadruple Comfort", price: "Rs. 5500", img: "https://images.unsplash.com/photo-1560185127-6ed189bf02f4?w=800&q=80", desc: "4 beds, ideal for large families.", badge: null },
    { id: 103, name: "Triple Deluxe", price: "Rs. 4500", img: "https://images.unsplash.com/photo-1611892440504-42a792e24d32?w=800&q=80", desc: "One double and one single bed configuration.", badge: null },
  ];

  const currentRooms = roomCategory === 'luxury' ? luxuryRooms : familyRooms;

  return (
    <div className="font-sans text-gray-900 antialiased bg-gray-50 selection:bg-orange-500 selection:text-white">
      
      {/* Navigation */}
      <nav 
        className={`fixed w-full z-50 transition-all duration-500 ${
          isScrolled ? 'bg-black/95 backdrop-blur-md shadow-2xl py-3 border-b border-orange-900/30' : 'bg-transparent py-6'
        }`}
      >
        <div className="container mx-auto px-6 flex justify-between items-center">
          <div className="flex items-center gap-3">
            <div className="bg-gradient-to-br from-amber-400 to-orange-600 p-2.5 rounded-xl shadow-lg shadow-orange-500/20">
              <Star className="text-white w-6 h-6 fill-current" />
            </div>
            <div>
              <h1 className="text-2xl font-bold tracking-tight text-white leading-none">
                GOKUL RAJ
              </h1>
              <span className="text-amber-500 text-[10px] tracking-[0.2em] uppercase font-bold block mt-1">
                Luxury Hotel
              </span>
            </div>
          </div>

          <div className="hidden md:flex space-x-10 items-center">
            {['Home', 'About', 'Gallery'].map((item) => (
              <a key={item} href={`#${item.toLowerCase()}`} className="text-gray-300 hover:text-white text-sm font-medium tracking-wide transition-colors relative group">
                {item}
                <span className="absolute -bottom-1 left-0 w-0 h-0.5 bg-orange-500 transition-all group-hover:w-full"></span>
              </a>
            ))}
            <button onClick={() => setShowServicesContent(true)} className="text-gray-300 hover:text-white text-sm font-medium tracking-wide transition-colors">Services</button>
            <a href="#contact" className="bg-gradient-to-r from-orange-600 to-amber-600 hover:from-orange-500 hover:to-amber-500 text-white px-7 py-3 rounded-full font-bold text-xs uppercase tracking-widest transition-all shadow-lg hover:shadow-orange-500/40 border border-orange-500/50">
              Book Now
            </a>
          </div>

          <button className="md:hidden text-white" onClick={() => setMobileMenuOpen(!mobileMenuOpen)}>
            {mobileMenuOpen ? <X size={28} /> : <Menu size={28} />}
          </button>
        </div>
        
        {/* Mobile Menu */}
        {mobileMenuOpen && (
          <div className="md:hidden bg-black/95 backdrop-blur-xl absolute w-full top-full left-0 border-t border-gray-800 shadow-2xl h-screen z-50">
            <div className="flex flex-col p-8 space-y-6 text-center">
              <a href="#home" onClick={() => setMobileMenuOpen(false)} className="text-white hover:text-orange-500 text-xl font-medium">Home</a>
              <a href="#rooms" onClick={() => setMobileMenuOpen(false)} className="text-white hover:text-orange-500 text-xl font-medium">Rooms</a>
              <button onClick={() => {setShowServicesContent(true); setMobileMenuOpen(false);}} className="text-white hover:text-orange-500 text-xl font-medium w-full">Services</button>
              <a href="#contact" onClick={() => setMobileMenuOpen(false)} className="text-orange-500 text-xl font-bold">Book Now</a>
            </div>
          </div>
        )}
      </nav>

      {/* 1. HERO SECTION - Reduced Height with Red Line Border */}
      <section 
        id="home" 
        className="relative pt-32 pb-20 flex items-center justify-center overflow-hidden bg-black border-b-8 border-[#FF5733]" 
        /* Using a custom hex or orange-500/red-500 to match the 'red line' description */
      >
        {/* Dynamic Gradient Background */}
        <div className="absolute inset-0 bg-[radial-gradient(ellipse_at_center,_var(--tw-gradient-stops))] from-gray-800 via-black to-black opacity-80"></div>
        <div className="absolute inset-0 bg-gradient-to-b from-black/60 via-transparent to-orange-950/20"></div>
        
        {/* Decorative Circles */}
        <div className="absolute top-1/4 left-1/4 w-96 h-96 bg-orange-500/10 rounded-full blur-[100px] animate-pulse"></div>
        <div className="absolute bottom-1/4 right-1/4 w-96 h-96 bg-amber-500/10 rounded-full blur-[100px] delay-700 animate-pulse"></div>

        <div className="relative z-10 container mx-auto px-6 text-center">
          <div className="inline-flex items-center gap-2 py-1 px-4 rounded-full bg-white/5 border border-white/10 backdrop-blur-sm text-amber-400 text-xs font-bold tracking-widest mb-8 uppercase animate-fade-in-up">
            <Star size={12} fill="currentColor" /> Madhubani's Premium Choice
          </div>
          <h1 className="text-5xl md:text-8xl font-bold text-white mb-6 leading-tight drop-shadow-2xl font-serif">
            Welcome to <br /> 
            <span className="text-transparent bg-clip-text bg-gradient-to-r from-amber-200 via-orange-300 to-amber-200 animate-shimmer bg-[length:200%_auto]">
              Gokul Raj
            </span>
          </h1>
          <p className="text-gray-400 max-w-xl mx-auto text-lg font-light px-4">
            Experience the perfect blend of traditional hospitality and modern luxury.
          </p>
        </div>
      </section>

      {/* 2. ROOMS SECTION - The Product (Moved to Top) */}
      <section id="rooms" className="py-20 bg-white relative">
        <div className="container mx-auto px-6 relative z-10">
          
          {/* HEADER: Centered on Mobile, Left/Right on Desktop */}
          <div className="flex flex-col md:flex-row justify-between items-center md:items-end mb-12 gap-8 text-center md:text-left">
            <div className="w-full md:w-auto">
              <span className="text-orange-600 font-bold uppercase tracking-widest text-sm mb-2 block">Accommodations</span>
              <h2 className="text-4xl md:text-5xl font-bold text-black font-serif">Curated Rooms</h2>
              <div className="w-24 h-1.5 bg-gradient-to-r from-orange-500 to-amber-500 rounded-full mt-4 mx-auto md:mx-0"></div>
            </div>
            
            {/* Elegant Category Switcher - Centered on Mobile */}
            <div className="bg-gray-100 p-1.5 rounded-full flex gap-2 shadow-inner mx-auto md:mx-0">
              <button 
                onClick={() => setRoomCategory('luxury')}
                className={`px-6 py-2.5 rounded-full text-sm font-bold transition-all duration-300 ${
                  roomCategory === 'luxury' 
                  ? 'bg-black text-white shadow-lg' 
                  : 'text-gray-500 hover:text-black'
                }`}
              >
                Luxury
              </button>
              <button 
                onClick={() => setRoomCategory('family')}
                className={`px-6 py-2.5 rounded-full text-sm font-bold transition-all duration-300 ${
                  roomCategory === 'family' 
                  ? 'bg-black text-white shadow-lg' 
                  : 'text-gray-500 hover:text-black'
                }`}
              >
                Family
              </button>
            </div>
          </div>

          <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-10">
            {currentRooms.map((room) => (
              <div key={room.id} className="group bg-white rounded-2xl overflow-hidden hover:shadow-[0_20px_50px_rgba(0,0,0,0.1)] transition-all duration-500 border border-gray-100">
                <div className="relative h-72 overflow-hidden">
                  <img 
                    src={room.img} 
                    alt={room.name} 
                    className="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
                  />
                  {/* Badge */}
                  {room.badge && (
                    <div className="absolute top-4 left-4 bg-orange-600 text-white text-[10px] font-bold px-3 py-1 rounded-full uppercase tracking-wider shadow-lg">
                      {room.badge}
                    </div>
                  )}
                  {/* Price Tag Overlay */}
                  <div className="absolute bottom-0 left-0 w-full bg-gradient-to-t from-black/80 to-transparent p-6 pt-20">
                    <p className="text-white text-xl font-bold">{room.price} <span className="text-xs font-normal opacity-70">/ night</span></p>
                  </div>
                </div>
                <div className="p-8">
                  <h3 className="text-2xl font-bold text-gray-900 mb-3 font-serif group-hover:text-orange-600 transition-colors">{room.name}</h3>
                  <p className="text-gray-500 text-sm mb-6 leading-relaxed line-clamp-2">{room.desc}</p>
                  
                  <div className="flex items-center justify-between pt-6 border-t border-gray-100">
                    <div className="flex gap-4 text-gray-400">
                      <Wifi size={18} className="hover:text-orange-500 transition-colors" />
                      <Coffee size={18} className="hover:text-orange-500 transition-colors" />
                      <BedDouble size={18} className="hover:text-orange-500 transition-colors" />
                    </div>
                    <button className="flex items-center gap-2 text-sm font-bold text-black group-hover:text-orange-600 transition-colors">
                      Book Now <ArrowRight size={16} />
                    </button>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* 3. CONCIERGE PANEL (The "Two Box" Section) */}
      <section className="bg-gray-50 py-16 relative overflow-hidden">
        <div className="absolute top-0 right-0 w-64 h-64 bg-orange-200/20 rounded-full blur-3xl"></div>
        <div className="absolute bottom-0 left-0 w-64 h-64 bg-amber-200/20 rounded-full blur-3xl"></div>
        
        <div className="container mx-auto px-6 relative z-10">
          <div className="bg-black text-white rounded-[2.5rem] p-8 md:p-10 shadow-2xl relative overflow-hidden border border-gray-800">
            {/* Background Pattern */}
            <div className="absolute inset-0 opacity-10" style={{backgroundImage: 'radial-gradient(#d97706 1px, transparent 1px)', backgroundSize: '30px 30px'}}></div>

            <div className="grid md:grid-cols-2 gap-12 items-center relative z-10">
              <div className="text-center md:text-left">
                <h3 className="text-3xl md:text-5xl font-bold mb-6 font-serif leading-tight">
                  How can we <br /><span className="text-orange-500">serve you</span> today?
                </h3>
                <p className="text-gray-400 text-lg mb-8 leading-relaxed">
                  Whether you are planning a grand wedding, a corporate seminar, or a relaxing weekend getaway, our concierge team is ready.
                </p>
                <div className="flex flex-col sm:flex-row gap-4">
                  <button 
                    onClick={() => document.getElementById('contact-box').scrollIntoView({ behavior: 'smooth' })}
                    className="flex-1 bg-gradient-to-r from-orange-600 to-orange-500 hover:from-orange-500 hover:to-orange-400 text-white py-5 px-8 rounded-2xl font-bold text-lg shadow-lg shadow-orange-500/30 transition-all transform hover:-translate-y-1 flex items-center justify-center gap-3"
                  >
                    <BedDouble size={24} /> Book a Stay
                  </button>
                  <button 
                    onClick={() => setShowServicesContent(true)}
                    className="flex-1 bg-white/10 hover:bg-white/20 backdrop-blur-md border border-white/20 text-white py-5 px-8 rounded-2xl font-bold text-lg transition-all transform hover:-translate-y-1 flex items-center justify-center gap-3"
                  >
                    <ChefHat size={24} /> Explore Services
                  </button>
                </div>
              </div>

              {/* Feature List */}
              <div className="grid grid-cols-2 gap-4">
                {[
                  { icon: <ShieldCheck size={28} />, title: "Safe & Sanitized", desc: "Best-in-class hygiene standards" },
                  { icon: <Star size={28} />, title: "Top Rated", desc: "Most loved hotel in Madhubani" },
                  { icon: <Users size={28} />, title: "Event Experts", desc: "Specialists in Weddings & Seminars" },
                  { icon: <PhoneCall size={28} />, title: "24/7 Support", desc: "Always here to help you" },
                ].map((feature, i) => (
                  <div key={i} className="bg-white/5 border border-white/10 p-6 rounded-2xl hover:bg-white/10 transition-colors">
                    <div className="text-orange-400 mb-3">{feature.icon}</div>
                    <h4 className="font-bold text-white mb-1">{feature.title}</h4>
                    <p className="text-xs text-gray-400">{feature.desc}</p>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* 4. CONTACT / TRUST BOX */}
      <section id="contact-box" className="py-20 bg-white">
        <div className="container mx-auto px-6">
          <div className="max-w-4xl mx-auto bg-white rounded-3xl shadow-[0_10px_60px_-15px_rgba(0,0,0,0.1)] border border-gray-100 overflow-hidden">
            <div className="flex flex-col md:flex-row">
              <div className="bg-black p-10 md:w-2/5 flex flex-col justify-center text-white relative overflow-hidden">
                <div className="absolute top-0 right-0 w-32 h-32 bg-orange-500/20 rounded-full blur-2xl -mr-10 -mt-10"></div>
                <h4 className="text-orange-400 font-bold uppercase tracking-widest text-xs mb-4">Reservations</h4>
                <div className="flex items-center gap-4 mb-6">
                   <PhoneCall className="text-white w-10 h-10 animate-pulse" />
                   <h2 className="text-3xl font-bold">+91 8797125005</h2>
                </div>
                <p className="text-gray-400 text-sm">Call us directly for the best rates.</p>
              </div>
              
              <div className="p-10 md:w-3/5 flex flex-col justify-center bg-orange-50/50">
                <div className="flex items-start gap-4 mb-4">
                  <div className="bg-green-100 text-green-700 p-2 rounded-full">
                    <CheckCircle size={20} />
                  </div>
                  <div>
                    <h5 className="font-bold text-gray-900">Verified Excellence</h5>
                    <p className="text-sm text-gray-500">"The hospitality at Gokul Raj is unmatched in the region. Highly recommended for families."</p>
                    <div className="flex gap-1 mt-2">
                      {[1,2,3,4,5].map(s => <Star key={s} size={12} className="text-amber-400 fill-current" />)}
                      <span className="text-xs text-gray-400 ml-2">- Recent Guest</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* 5. GALLERY SLIDER - Visual Immersion */}
      <section id="gallery" className="py-24 bg-black relative">
        <div className="container mx-auto px-6">
          <div className="flex items-end justify-between mb-12">
            <div>
              <span className="text-orange-500 font-bold uppercase tracking-widest text-sm mb-2 block">Our Gallery</span>
              <h2 className="text-4xl font-bold text-white font-serif">A Glimpse of Luxury</h2>
            </div>
            <div className="hidden md:flex gap-2">
              <button onClick={prevSlide} className="p-3 rounded-full border border-gray-700 text-white hover:bg-orange-600 hover:border-orange-600 transition-all"><ChevronLeft /></button>
              <button onClick={nextSlide} className="p-3 rounded-full border border-gray-700 text-white hover:bg-orange-600 hover:border-orange-600 transition-all"><ChevronRight /></button>
            </div>
          </div>
          
          <div className="relative w-full h-[500px] rounded-3xl overflow-hidden shadow-2xl group">
            <div className="absolute inset-0 transition-transform duration-1000 ease-out">
              <img 
                key={currentSlide}
                src={gallerySlides[currentSlide].image} 
                alt={gallerySlides[currentSlide].title} 
                className="w-full h-full object-cover animate-fade-in"
              />
              <div className="absolute inset-0 bg-gradient-to-t from-black via-black/20 to-transparent"><