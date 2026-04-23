```datacorejsx
return function View() {
  const pages = dc.useQuery('@page and path("Health")');

  if (!pages || pages.length === 0) {
    return <div className="ah-card">No health data found.</div>;
  }

  const sorted = [...pages].sort((a, b) => {
    const da = new Date(a.$frontmatter.date.value ?? a.$ctime ?? 0).getTime();
    const db = new Date(b.$frontmatter.date.value ?? b.$ctime ?? 0).getTime();
    return db - da;
  });

  const latest = sorted[0];
  const recent = sorted.slice(0, 6).reverse();

  const move = Number(latest.$frontmatter.move.value ?? 0);
  const moveGoal = Number(latest.$frontmatter.move_goal.value ?? 500);

  const exercise = Number(latest.$frontmatter.exercise.value ?? 0);
  const exerciseGoal = Number(latest.$frontmatter.exercise_goal.value ?? 30);

  const stand = Number(latest.$frontmatter.stand.value ?? 0);
  const standGoal = Number(latest.$frontmatter.stand_goal.value ?? 12);

  const hrLow = Number(latest.$frontmatter.hr_low.value ?? 0);
  const hrAvg = Number(latest.$frontmatter.hr_avg.value ?? 0);
  const hrHigh = Number(latest.$frontmatter.hr_high.value ?? 0);
  const hrResting = Number(latest.$frontmatter.hr_resting.value ?? 57);

  const movePct = moveGoal > 0 ? Math.min(move / moveGoal, 1) : 0;
  const exercisePct = exerciseGoal > 0 ? Math.min(exercise / exerciseGoal, 1) : 0;
  const standPct = standGoal > 0 ? Math.min(stand / standGoal, 1) : 0;

  const moveDeg = movePct * 360;
  const exerciseDeg = exercisePct * 360;
  const standDeg = standPct * 360;

  const allHighs = recent.map(d => Number(d.$frontmatter.hr_high.value ?? 0));
  const chartMax = Math.max(200, ...allHighs);
  const chartMin = 40;

  function scale(value) {
    const n = Number(value ?? 0);
    const clamped = Math.max(chartMin, Math.min(chartMax, n));
    return ((clamped - chartMin) / (chartMax - chartMin)) * 100;
  }

  function shortDate(value) {
    if (!value) return "";
    const d = new Date(value);
    if (isNaN(d.getTime())) return String(value);
    return d.toLocaleDateString("en-US", {
      month: "short",
      day: "numeric"
    });
  }

  return (
    <div className="ah-card">
      <div className="ah-header">
        <div className="ah-title">Today's Activity</div>
        <div className="ah-subtitle">
          Apple Health style activity rings and heart rate summary
        </div>
      </div>

      <div className="ah-rings-wrap">
        <div className="ah-rings">
          <div
            className="ah-ring ah-ring-move"
            style={{ "--deg": `${moveDeg}deg` }}
          ></div>

          <div
            className="ah-ring ah-ring-exercise"
            style={{ "--deg": `${exerciseDeg}deg` }}
          ></div>

          <div
            className="ah-ring ah-ring-stand"
            style={{ "--deg": `${standDeg}deg` }}
          ></div>

          <div className="ah-ring-center">
            <div className="ah-center-stat ah-center-move">
              {move}/{moveGoal} CAL
            </div>
            <div className="ah-center-stat ah-center-exercise">
              {exercise}/{exerciseGoal} MIN
            </div>
            <div className="ah-center-stat ah-center-stand">
              {stand}/{standGoal} HR
            </div>
          </div>
        </div>
      </div>

      <div className="ah-metric-row">
        <div className="ah-metric">
          <div className="ah-metric-value ah-move-text">{move}</div>
          <div className="ah-metric-label">MOVE · /{moveGoal}</div>
        </div>

        <div className="ah-metric">
          <div className="ah-metric-value ah-exercise-text">{exercise}</div>
          <div className="ah-metric-label">EXERCISE · /{exerciseGoal}</div>
        </div>

        <div className="ah-metric">
          <div className="ah-metric-value ah-stand-text">{stand}</div>
          <div className="ah-metric-label">STAND · /{standGoal}</div>
        </div>
      </div>

      <div className="ah-chart-section">
        <div className="ah-chart-box">
          <div className="ah-grid-lines">
            <div className="ah-grid-line"></div>
            <div className="ah-grid-line"></div>
            <div className="ah-grid-line"></div>
            <div className="ah-grid-line"></div>
          </div>

          <div
            className="ah-resting-line"
            style={{ bottom: `${scale(hrResting)}%` }}
          >
            <span>resting ~{hrResting}</span>
          </div>

          <div className="ah-chart-columns">
            {recent.map(day => {
              const low = Number(day.$frontmatter.hr_low.value ?? 0);
              const avg = Number(day.$frontmatter.hr_avg.value ?? 0);
              const high = Number(day.$frontmatter.hr_high.value ?? 0);

              const lowPct = scale(low);
              const highPct = scale(high);
              const rangeHeight = Math.max(8, highPct - lowPct);

              const avgPosWithinRange =
                high === low
                  ? 50
                  : ((avg - low) / (high - low)) * 100;

              const avgClamped = Math.max(0, Math.min(100, avgPosWithinRange));

              return (
                <div className="ah-chart-col">
                  <div className="ah-chart-plot">
                    <div
                      className="ah-range-bar"
                      style={{
                        bottom: `${lowPct}%`,
                        height: `${rangeHeight}%`
                      }}
                    >
                      <div
                        className="ah-range-dot"
                        style={{ bottom: `${avgClamped}%` }}
                      ></div>
                    </div>
                  </div>
                  <div className="ah-chart-date">{shortDate(day.$frontmatter.date.value)}</div>
                </div>
              );
            })}
          </div>
        </div>
      </div>

      <div className="ah-bottom-stats">
        <div className="ah-bottom-stat">
          <div className="ah-bottom-value ah-low-text">{hrLow}</div>
          <div className="ah-bottom-label">LOWEST</div>
        </div>

        <div className="ah-bottom-stat">
          <div className="ah-bottom-value ah-avg-text">{hrAvg}</div>
          <div className="ah-bottom-label">HEART RATE AVG</div>
        </div>

        <div className="ah-bottom-stat">
          <div className="ah-bottom-value ah-high-text">{hrHigh}</div>
          <div className="ah-bottom-label">HIGHEST</div>
        </div>
      </div>
    </div>
  );
}
```
