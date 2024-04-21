<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Overhead Tank Progress Monitor</title>
<style>
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #87CEEB; /* Light blue resembling water */
  }
  
  .container {
    max-width: 600px;
    margin: 20px auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #fff; /* White background for tanks */
  }

  .tank {
    width: 100%;
    background-color: #f2f2f2;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 10px;
    margin-bottom: 20px;
  }

  .tank-name {
    font-weight: bold;
    margin-bottom: 10px;
  }

  .progress-bar {
    width: 100%;
    background-color: #ddd;
    border: 1px solid #bbb;
    border-radius: 4px;
    height: 20px;
    margin-bottom: 10px;
    position: relative;
  }

  .progress {
    background-color: #4caf50;
    height: 100%;
    border-radius: 4px;
  }

  .progress-text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: #333;
  }

  .latest-activity {
    margin-top: 10px;
    font-size: 14px;
  }

  @media screen and (max-width: 768px) {
    .container {
      width: 90%;
    }
  }
</style>
</head>
<body>

<div class="container" id="tankContainer">
</div>

<script>
  // JavaScript to dynamically generate tanks and update progress and latest activity
  
  // Function to add a new tank with given ID
  function addTank(tankId) {
    var tankName = prompt("Enter the name for Tank " + tankId);
    if (tankName) {
        var inchargeName = prompt("Enter the incharge name for Tank " + tankId);
        if (inchargeName) {
            var inchargePhone = prompt("Enter the incharge phone number for Tank " + tankId);
            if (inchargePhone) {
                var startDate = prompt("Enter the start date for Tank " + tankId + " (YYYY-MM-DD)");
                if (startDate) {
                    // Create tank HTML elements
                    var tankDiv = document.createElement("div");
                    tankDiv.className = "tank";
                    tankDiv.innerHTML = `
                      <div class="tank-name">${tankName}</div>
                      <div>Incharge Name: ${inchargeName}</div>
                      <div>Incharge Phone: ${inchargePhone}</div>
                      <div>Start Date: ${startDate}</div>
                      <div class="progress-bar">
                        <div class="progress" id="progress${tankId}" style="width: 0%;"></div>
                        <div class="progress-text" id="progressText${tankId}">0%</div>
                      </div>
                      <div class="latest-activity" id="activity${tankId}">Latest Activity: Not updated</div>
                      <div>
                        <button onclick="editProgress(${tankId})">Edit Completion Percentage</button>
                        <button onclick="editActivity(${tankId})">Edit Latest Activity</button>
                      </div>
                    `;

                    // Append tank to container
                    document.getElementById("tankContainer").appendChild(tankDiv);
                } else {
                    alert("Please enter the start date for Tank " + tankId);
                }
            } else {
                alert("Please enter the incharge phone number for Tank " + tankId);
            }
        } else {
            alert("Please enter the incharge name for Tank " + tankId);
        }
    }
  }

  var totalTanks = prompt("Enter the total number of tanks you want to track:");
  if (totalTanks && !isNaN(totalTanks) && totalTanks > 0) {
    for (var i = 1; i <= totalTanks; i++) {
      addTank(i);
    }
  } else {
    alert("Please enter a valid number greater than 0.");
  }

  // Function to edit completion percentage
  function editProgress(tankId) {
    var progress = prompt("Enter the new completion percentage for Tank " + tankId);
    if (progress && !isNaN(progress) && progress >= 0 && progress <= 100) {
      document.getElementById("progress" + tankId).style.width = progress + "%";
      document.getElementById("progressText" + tankId).innerText = progress + "%";
    } else {
      alert("Please enter a valid percentage between 0 and 100.");
    }
  }

  // Function to edit latest activity
  function editActivity(tankId) {
    var latestActivity = prompt("Enter the latest activity for Tank " + tankId);
    if (latestActivity) {
      document.getElementById("activity" + tankId).innerText = "Latest Activity: " + latestActivity;
    }
  }
</script>

</body>
</html>
