==============================================================
 CAPACITY CONTROL ROOM  (hospital-flow.html)
 Synesis 26 hackathon demo
==============================================================

A single-file, browser-based decision-support dashboard that helps
hospital operations teams spot capacity bottlenecks early and act on
them. It simulates a hospital, forecasts emergency department (ED)
demand, and recommends safe, rule-checked actions that a clinician
approves with one tap.

DISCLAIMER: All data is synthetic. This is a hackathon demo for
decision support only. It is NOT for clinical use.


--------------------------------------------------------------
 WHAT IT DOES
--------------------------------------------------------------

* Simulates a hospital hour by hour: ED, CT scanner, and five wards
  (ICU, Medical, Surgical, Paediatrics, Maternity).
* Forecasts ED arrivals for the next 12 hours, with a 90% range.
* Predicts ward occupancy 6 hours ahead.
* Generates prioritised recommendations (P1 = urgent, P2 = soon),
  each with a reason, expected impact and safety note.
* Waits for human approval before anything changes
  (human-in-the-loop).
* Compares two hospitals fed the identical patient stream:
  one acting on your approvals, one doing nothing (baseline).
* Keeps a decision log of everything approved or dismissed.


--------------------------------------------------------------
 HOW TO RUN
--------------------------------------------------------------

No install, no build step, no dependencies.

1. Download or clone this repository.
2. Open hospital-flow.html in any modern browser
   (Chrome, Edge, Firefox, Safari).

The only external resource is the Atkinson Hyperlegible font from
Google Fonts. If you are offline, the page falls back to the system
font and works normally.

Publish with GitHub Pages (optional):
1. Rename hospital-flow.html to index.html (or keep the name and
   link to it directly).
2. Repo Settings > Pages > Source: "Deploy from a branch" >
   branch "main", folder "/ (root)" > Save.
3. Your demo will be live at:
   https://<your-username>.github.io/<repo-name>/


--------------------------------------------------------------
 HOW TO USE THE DEMO
--------------------------------------------------------------

Top bar controls:
  Play / Pause   Run the simulation continuously.
  +1 hour        Advance the clock one hour manually.
  Speed          Choose 1x or 3x simulation speed.
  Surge          Inject 6 hours of heavy arrivals (1.6x demand)
                 to stress-test the hospital.
  Auto-approve   Demo only. Automatically approves every
                 recommendation (skips the human check).
  Reset          Restart the simulation from the beginning.

Suggested walkthrough:
  1. Press Play and watch the KPIs, ED chart and ward bars.
  2. Press "Surge" to trigger a demand spike.
  3. Review the "Recommended actions" cards and press Approve or
     Dismiss on each one.
  4. Check the "Impact" panel to see how your approvals compare
     with the do-nothing baseline.


--------------------------------------------------------------
 DASHBOARD SECTIONS
--------------------------------------------------------------

KPIs                  Headline numbers for the current state.
Recommended actions   Approve / dismiss cards, sorted by priority.
Alerts                Forecast warnings (ward near full, ED demand
                      exceeding staffed bays, arrival surge).
ED arrivals chart     Last 24h actual (grey bars), typical value for
                      that weekday and hour (dashed), and forecast
                      with 90% range (teal).
Staff and equipment   ED nurses, bays, CT and X-ray utilisation.
Wards                 Occupied beds (bar), staffed limit (black
                      tick), 6-hour forecast (circle), plus ED
                      boarders waiting for that ward.
Impact                Baseline vs. your approvals, same patients.
Decision log          Recent approvals and dismissals.


--------------------------------------------------------------
 TYPES OF RECOMMENDATIONS
--------------------------------------------------------------

* Move a nurse between wards and the ED to open staffed beds.
* Expedite discharges for patients already cleared to leave.
* Transfer stable patients to a safe overflow ward.
* Boost CT throughput for 6 hours when the scan backlog grows.
* Escalate to the bed manager when no safe overflow option exists.


--------------------------------------------------------------
 HOW IT WORKS
--------------------------------------------------------------

Data
  Synthetic. Six weeks of hourly ED arrivals with daily and weekly
  patterns train the forecast.

Forecast
  Typical arrivals for each weekday and hour, scaled by a live level
  that adapts when real arrivals run higher or lower than expected.

Patients
  Each patient arrives with an acuity (1 = most urgent), waits in a
  queue, gets an ED bay, may need CT, and is then discharged or
  admitted. Admitted patients board in the ED until a staffed ward
  bed is available.

Rules engine
  Every recommendation comes from a detected bottleneck and is
  checked against hard safety limits:
    - Safe nurse-to-patient ratios, plus a 2-patient buffer on any
      donor ward.
    - ICU, Paediatrics and Maternity never donate staff.
    - Only patients with a signed discharge order are expedited.
    - Only stable patients close to discharge or step-down are
      transferred, and only to pre-defined safe overflow wards.

Human in the loop
  Nothing changes until a clinician taps Approve.


--------------------------------------------------------------
 TECH
--------------------------------------------------------------

* Plain HTML, CSS and JavaScript in one file. No frameworks.
* Charts drawn as inline SVG.
* Seeded random generators, so results are reproducible.
* Light and dark theme (follows your system setting).
* Responsive layout for desktop and mobile; respects
  reduced-motion preferences.


--------------------------------------------------------------
 FILES
--------------------------------------------------------------

  hospital-flow.html   The whole application.
  README.txt           This file.


--------------------------------------------------------------
 LIMITATIONS
--------------------------------------------------------------

* Simplified model; real hospitals are far more complex.
* Staffing, bed counts and rates are illustrative assumptions.
* Not validated, certified or approved for clinical use.


--------------------------------------------------------------
 LICENSE
--------------------------------------------------------------

Add your preferred license here (for example MIT) and include a
LICENSE file in the repository.
