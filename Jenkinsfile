echo "===== Step 1: Clean Workspace ====="
rm -rf maven-pro
rm -rf target

echo "===== Step 2: Clone Git Repository ====="
git clone -b main https://github.com/bhargavisirigiri/maven-pro.git

cd maven-pro

echo "===== Step 3: Maven Build (WAR) ====="
mvn clean package

if [ $? -ne 0 ]; then
  echo "Maven build failed!"
  exit 1
fi

echo "===== Step 4: Find WAR File ====="
WAR_FILE=$(find target -name "*.war" | head -n 1)

if [ -z "$WAR_FILE" ]; then
  echo "No WAR file found! Build failed."
  exit 1
fi

echo "WAR File Found: $WAR_FILE"

echo "===== Step 5: Deploying to Tomcat ====="
curl -u admin:StrongPassword123 \
     -T "$WAR_FILE" \
     "http://44.255.180.0:8080/manager/text/deploy?path=/myapp&update=true"

if [ $? -eq 0 ]; then
   echo "===== Deployment Successful ====="
else
   echo "===== Deployment FAILED ====="
   exit 1
fi

