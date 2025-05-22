# NeoRide - Safe and Reliable Ride Booking Platform

NeoRide is a modern, frontend-only ride booking platform designed for safe and convenient transportation experiences. This GitHub repository contains a complete single-page web application that allows users to book rides, view their scheduled rides, rate drivers, and read driver reviews — all without any backend or server dependency.

## Features

- Book rides by entering pickup and dropoff locations, date, and time.
- View a list of all your upcoming rides.
- Rate drivers with star ratings and leave reviews.
- Store rides and ratings locally in your browser using localStorage.
- Elegant, modern, and user-friendly interface.
- Responsive design suitable for desktops and mobile devices.
- All code contained in a single HTML file for easy deployment and demo.

## Technologies Used

- HTML5 (semantic structure)
- <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>NeoRide - Safe and Reliable Ride Booking</title>
  <style>
    /* RESET */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background: linear-gradient(135deg, #1e3c72, #2a5298);
      color: #f1f1f1;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px;
      user-select: none;
    }

    h1 {
      font-weight: 700;
      font-size: 3rem;
      margin-bottom: 10px;
      text-align: center;
      text-shadow: 2px 2px 8px rgba(0,0,0,0.5);
    }

    h2 {
      margin-top: 30px;
      margin-bottom: 15px;
      font-weight: 600;
      border-bottom: 2px solid #00c6ff;
      padding-bottom: 5px;
      text-align: center;
      max-width: 500px;
      width: 100%;
    }

    .container {
      background: rgba(0,0,0,0.4);
      border-radius: 14px;
      padding: 25px 30px;
      max-width: 540px;
      width: 100%;
      box-shadow: 0 4px 20px rgba(0,0,0,0.5);
      margin-bottom: 40px;
    }

    form {
      display: flex;
      flex-direction: column;
      gap: 15px;
    }

    label {
      font-weight: 600;
      font-size: 1.1rem;
      margin-bottom: 4px;
      color: #a0eaff;
    }

    input, select, textarea {
      border-radius: 8px;
      border: none;
      padding: 12px 15px;
      font-size: 1rem;
      outline: none;
      transition: all 0.3s ease;
      background-color: #2a5298;
      color: #fff;
      box-shadow: inset 0 0 5px rgba(255,255,255,0.15);
      resize: vertical;
    }

    input::placeholder, textarea::placeholder {
      color: #c4d8e9;
      font-style: italic;
    }

    input:focus, select:focus, textarea:focus {
      background-color: #007acc;
      box-shadow: 0 0 8px #00c6ff;
      color: #e0f7ff;
    }

    button {
      background: #00c6ff;
      border: none;
      padding: 15px;
      font-weight: 700;
      font-size: 1.2rem;
      border-radius: 10px;
      cursor: pointer;
      color: #022c43;
      box-shadow: 0 8px 15px rgba(0, 198, 255, 0.4);
      transition: all 0.2s ease-in-out;
      user-select: none;
      align-self: center;
      max-width: 200px;
    }

    button:hover {
      background: #00a4d8;
      box-shadow: 0 12px 22px rgba(0, 164, 216, 0.6);
      transform: translateY(-2px);
    }

    .rides-list {
      list-style-type: none;
      max-height: 300px;
      overflow-y: auto;
      border-radius: 10px;
      box-shadow: inset 0 0 15px rgba(0,0,0,0.6);
      background: #13294b;
      padding: 10px 15px;
    }

    .ride-item {
      background: #1f3a70;
      border-radius: 10px;
      margin-bottom: 15px;
      padding: 15px;
      cursor: pointer;
      box-shadow: 0 3px 7px rgba(0,198,255,0.3);
      transition: background-color 0.3s ease;
      position: relative;
    }

    .ride-item:hover {
      background: #007acc;
    }

    .ride-header {
      font-weight: 700;
      font-size: 1.1rem;
      margin-bottom: 4px;
      color: #00e5ff;
    }

    .ride-details {
      font-size: 0.9rem;
      opacity: 0.8;
    }

    .no-rides {
      text-align: center;
      font-style: italic;
      color: #66cfff;
      margin-top: 15px;
    }

    /* Rating Modal */

    .modal-overlay {
      position: fixed;
      top: 0; left: 0; right: 0; bottom:0;
      background: rgba(0,0,0,0.7);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 1000;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s ease;
    }

    .modal-overlay.active {
      opacity: 1;
      pointer-events: all;
    }

    .modal {
      background: #1e3c72;
      padding: 25px 30px;
      border-radius: 14px;
      max-width: 400px;
      width: 90%;
      box-shadow: 0 8px 30px rgba(0,198,255,0.5);
      color: #e0f7ff;
      position: relative;
      animation: slideDown 0.4s ease forwards;
    }

    @keyframes slideDown {
      from {
        transform: translateY(-20px);
        opacity: 0;
      }
      to {
        transform: translateY(0);
        opacity: 1;
      }
    }

    .modal h3 {
      margin-bottom: 15px;
      text-align: center;
      color: #00c6ff;
    }

    .stars {
      display: flex;
      justify-content: center;
      margin-bottom: 15px;
      gap: 8px;
      font-size: 2rem;
      cursor: pointer;
      user-select: none;
    }

    .star {
      color: #444;
      transition: color 0.3s ease;
    }

    .star.filled {
      color: #00e5ff;
      text-shadow: 0 0 6px #00e5ff;
    }

    .modal-textarea {
      width: 100%;
      height: 80px;
      padding: 10px 15px;
      border-radius: 10px;
      border: none;
      background-color: #2a5298;
      color: white;
      font-size: 1rem;
      resize: vertical;
      box-shadow: inset 0 0 8px rgba(0,198,255,0.5);
      margin-bottom: 20px;
      outline: none;
      transition: background-color 0.3s ease;
    }

    .modal-textarea:focus {
      background-color: #007acc;
      box-shadow: 0 0 10px #00c6ff;
    }

    .modal-buttons {
      text-align: center;
      display: flex;
      justify-content: center;
      gap: 20px;
    }

    .btn-cancel, .btn-submit {
      flex: 1;
      padding: 12px 0;
      font-weight: 700;
      font-size: 1.1rem;
      border-radius: 10px;
      user-select: none;
      cursor: pointer;
      border: none;
      transition: background-color 0.3s ease;
      box-shadow: 0 5px 15px rgba(0,198,255,0.4);
      color: #022c43;
    }

    .btn-submit {
      background: #00c6ff;
    }

    .btn-submit:hover {
      background: #00a4d8;
      box-shadow: 0 8px 22px rgba(0,164,216,0.6);
      transform: translateY(-2px);
      color: #e0f7ff;
    }

    .btn-cancel {
      background: #555;
      color: #ccc;
    }

    .btn-cancel:hover {
      background: #444;
      color: #e0f7ff;
    }

    /* Responsive */

    @media (max-width: 600px) {
      h1 {
        font-size: 2.4rem;
      }
      .container {
        padding: 20px;
      }
      button {
        max-width: 100%;
      }
    }

  </style>
</head>
<body>
  <h1>NeoRide 🚗 Safe Ride Booking</h1>

  <section class="container" id="booking-section">
    <h2>Book Your Ride</h2>
    <form id="booking-form" autocomplete="off">
      <div>
        <label for="pickup">Pickup Location</label>
        <input type="text" id="pickup" name="pickup" placeholder="Enter pickup location" required />
      </div>
      <div>
        <label for="dropoff">Dropoff Location</label>
        <input type="text" id="dropoff" name="dropoff" placeholder="Enter dropoff location" required />
      </div>
      <div>
        <label for="date">Date</label>
        <input type="date" id="date" name="date" required />
      </div>
      <div>
        <label for="time">Time</label>
        <input type="time" id="time" name="time" required />
      </div>
      <button type="submit">Book Ride</button>
    </form>
  </section>

  <section class="container" id="rides-section">
    <h2>My Rides</h2>
    <ul class="rides-list" id="rides-list">
      <!-- Ride items listed here -->
    </ul>
    <p class="no-rides" id="no-rides-message">No rides booked yet.</p>
  </section>

  <!-- Rating Modal -->
  <div class="modal-overlay" id="rating-modal">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modal-title">
      <h3 id="modal-title">Rate Your Driver</h3>
      <div class="stars" id="star-rating" aria-label="Star rating">
        <span class="star" data-value="1" role="button" tabindex="0" aria-pressed="false" aria-label="1 star">&#9733;</span>
        <span class="star" data-value="2" role="button" tabindex="0" aria-pressed="false" aria-label="2 stars">&#9733;</span>
        <span class="star" data-value="3" role="button" tabindex="0" aria-pressed="false" aria-label="3 stars">&#9733;</span>
        <span class="star" data-value="4" role="button" tabindex="0" aria-pressed="false" aria-label="4 stars">&#9733;</span>
        <span class="star" data-value="5" role="button" tabindex="0" aria-pressed="false" aria-label="5 stars">&#9733;</span>
      </div>
      <textarea class="modal-textarea" id="review-text" placeholder="Leave a review (optional)" aria-label="Driver review text"></textarea>
      <div class="modal-buttons">
        <button class="btn-submit" id="submit-rating-btn">Submit</button>
        <button class="btn-cancel" id="cancel-rating-btn">Cancel</button>
      </div>
    </div>
  </div>

  <script>
    (() => {
      // Elements
      const bookingForm = document.getElementById('booking-form');
      const ridesListEl = document.getElementById('rides-list');
      const noRidesMessage = document.getElementById('no-rides-message');
      const ratingModal = document.getElementById('rating-modal');
      const starRatingEl = document.getElementById('star-rating');
      const reviewTextEl = document.getElementById('review-text');
      const submitRatingBtn = document.getElementById('submit-rating-btn');
      const cancelRatingBtn = document.getElementById('cancel-rating-btn');

      // LocalStorage Keys
      const RIDES_KEY = 'neoride_rides';
      const DRIVERS_KEY = 'neoride_drivers';

      // Application state
      let rides = [];
      let currentRideIdBeingRated = null;
      let currentRating = 0;

      // Initialize app
      function init() {
        loadRides();
        renderRides();
        attachEventListeners();
      }

      // Load rides from localStorage
      function loadRides() {
        const ridesJSON = localStorage.getItem(RIDES_KEY);
        rides = ridesJSON ? JSON.parse(ridesJSON) : [];
      }

      // Save rides to localStorage
      function saveRides() {
        localStorage.setItem(RIDES_KEY, JSON.stringify(rides));
      }

      // Create a driver if not exists and return driverId
      function registerDriver(driverName = 'Default Driver') {
        // Since we do not have backend and users, a fixed driver name is used
        // Could be enhanced to simulate multiple drivers
        return driverName;
      }

      // Render rides list
      function renderRides() {
        ridesListEl.innerHTML = '';
        if (rides.length === 0) {
          noRidesMessage.style.display = 'block';
          return;
        }
        noRidesMessage.style.display = 'none';

        rides.forEach(ride => {
          const li = document.createElement('li');
          li.classList.add('ride-item');
          li.tabIndex = 0; // make focusable for accessibility
          li.setAttribute('role', 'button');
          li.setAttribute('aria-label', `Ride from ${ride.pickup} to ${ride.dropoff} on ${ride.date} at ${ride.time}. Click to rate driver.`);

          // Ride summary
          const header = document.createElement('div');
          header.classList.add('ride-header');
          header.textContent = `${ride.pickup} → ${ride.dropoff}`;

          // Ride details
          const details = document.createElement('div');
          details.classList.add('ride-details');
          details.innerHTML = `
            Date: ${ride.date} | Time: ${ride.time}<br>
            Rating: ${renderStarsInline(ride.rating)}<br>
            Review: ${ride.review ? escapeHtml(ride.review) : '<em>No review yet</em>'}
          `;

          li.appendChild(header);
          li.appendChild(details);

          // Click event to open rating modal
          li.addEventListener('click', () => openRatingModal(ride.id));
          li.addEventListener('keydown', (e) => {
            if(e.key === 'Enter' || e.key === ' ') {
              openRatingModal(ride.id);
              e.preventDefault();
            }
          });

          ridesListEl.appendChild(li);
        });
      }

      // Render stars inline small for list with filled stars
      function renderStarsInline(rating) {
        if (!rating) return '<span style="color:#666;">No rating</span>';
        let starsHTML = '';
        for(let i=1; i<=5; i++) {
          if(i <= rating) {
            starsHTML += '★';
          } else {
            starsHTML += '☆';
          }
        }
        return `<span style="color:#00e5ff; font-size:1.1rem; text-shadow: 0 0 4px #00e5ff;">${starsHTML}</span>`;
      }

      // Escape unsafe HTML characters to prevent injection
      function escapeHtml(text) {
        const div = document.createElement('div');
        div.textContent = text;
        return div.innerHTML;
      }

      // Attach event listeners
      function attachEventListeners() {
        bookingForm.addEventListener('submit', handleBookingSubmit);
        starRatingEl.addEventListener('click', handleStarClick);
        starRatingEl.addEventListener('keydown', handleStarKeyDown);
        submitRatingBtn.addEventListener('click', submitRating);
        cancelRatingBtn.addEventListener('click', closeRatingModal);

        // Close modal on overlay click
        ratingModal.addEventListener('click', (e) => {
          if (e.target === ratingModal) {
            closeRatingModal();
          }
        });

        // Keyboard accessibility for modal
        document.addEventListener('keydown', (e) => {
          if (e.key === 'Escape' && ratingModal.classList.contains('active')) {
            closeRatingModal();
          }
        });
      }

      // Handle booking form submission
      function handleBookingSubmit(e) {
        e.preventDefault();

        const pickup = bookingForm.pickup.value.trim();
        const dropoff = bookingForm.dropoff.value.trim();
        const date = bookingForm.date.value;
        const time = bookingForm.time.value;

        if(!pickup || !dropoff || !date || !time) {
          alert('Please fill in all booking fields.');
          return;
        }

        if(new Date(date + ' ' + time) < new Date()) {
          alert('Please select a future date and time for your ride.');
          return;
        }

        // Create new ride
        const newRide = {
          id: Date.now().toString(),
          pickup,
          dropoff,
          date,
          time,
          rating: null,
          review: ''
        };

        rides.push(newRide);
        saveRides();
        renderRides();

        // Reset form
        bookingForm.reset();
      }

      // Open rating modal for a ride
      function openRatingModal(rideId) {
        currentRideIdBeingRated = rideId;
        currentRating = 0;
        reviewTextEl.value = '';

        // Reset stars
        updateStarUI(0);

        ratingModal.classList.add('active');
        reviewTextEl.focus();
      }

      // Close rating modal
      function closeRatingModal() {
        currentRideIdBeingRated = null;
        currentRating = 0;
        reviewTextEl.value = '';
        ratingModal.classList.remove('active');
      }

      // Handle star rating click
      function handleStarClick(e) {
        if(e.target.classList.contains('star')) {
          const value = parseInt(e.target.dataset.value);
          currentRating = value;
          updateStarUI(value);
        }
      }

      // Keyboard accessible star rating (arrow keys + enter)
      function handleStarKeyDown(e) {
        const focusedStar = document.activeElement;
        if (!focusedStar.classList.contains('star')) return;

        let value = parseInt(focusedStar.dataset.value);

        if (e.key === 'ArrowRight' || e.key === 'ArrowUp') {
          if(value < 5) {
            const nextStar = starRatingEl.querySelector(`.star[data-value="${value + 1}"]`);
            nextStar.focus();
            currentRating = value + 1;
            updateStarUI(currentRating);
          }
          e.preventDefault();
        } else if (e.key === 'ArrowLeft' || e.key === 'ArrowDown') {
          if(value > 1) {
            const prevStar = starRatingEl.querySelector(`.star[data-value="${value - 1}"]`);
            prevStar.focus();
            currentRating = value - 1;
            updateStarUI(currentRating);
          }
          e.preventDefault();
        } else if (e.key === 'Enter' || e.key === ' ') {
          currentRating = value;
          updateStarUI(currentRating);
          e.preventDefault();
        }
      }

      // Update star highlights in UI
      function updateStarUI(rating) {
        [...starRatingEl.children].forEach(star => {
          const starValue = parseInt(star.dataset.value);
          if(starValue <= rating) {
            star.classList.add('filled');
            star.setAttribute('aria-pressed', 'true');
          } else {
            star.classList.remove('filled');
            star.setAttribute('aria-pressed', 'false');
          }
        });
      }

      // Submit rating and review
      function submitRating() {
        if(currentRideIdBeingRated === null) return;

        if(currentRating === 0) {
          alert('Please select a star rating before submitting.');
          return;
        }

        const rideIndex = rides.findIndex(r => r.id === currentRideIdBeingRated);
        if(rideIndex === -1) {
          alert('Ride not found.');
          closeRatingModal();
          return;
        }

        rides[rideIndex].rating = currentRating;
        rides[rideIndex].review = reviewTextEl.value.trim();

        saveRides();
        renderRides();
        closeRatingModal();
      }

      // Initialize app on DOM ready
      document.addEventListener('DOMContentLoaded', init);

    })();
  </script>
</body>
</html>

- CSS3 (modern styling with flexbox and animations)
- JavaScript (ES6+ for interactivity and localStorage persistence)
- No backend server required — runs entirely in the browser.

## Getting Started

1. Clone or download this repository.
2. Open the `index.html` file in any modern web browser (Chrome, Firefox, Edge, Safari).
3. Start booking rides, viewing your rides, and rating drivers instantly!

## How It Works

- When you submit a ride booking, it is saved in your browser's localStorage.
- You can see all scheduled rides listed on the "My Rides" section.
- Click on rides to rate the driver and leave feedback.
- Ratings and reviews are also saved locally allowing you to simulate driver feedback.
  
## Future Improvements

- Add real-time driver and ride tracking.
- Integrate real backend with user authentication.
- Add payment gateway integration.
- Expand with driver management features.

## Contributing

This repository is open for contributions! Feel free to fork and submit pull requests.

## Contact

For questions or support:
https://www.linkedin.com/in/jaideep-shekhawat-92075b221/
jaideep
---

Thank you for checking out NeoRide! Experience safe, reliable rides right from your browser.
