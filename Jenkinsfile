//node('fedora-atomic') {
node('master') {
    // Wait for message and store message content in variable
    def CI_MESSAGE = waitForCIMessage \
         providerName: 'fedora-fedmsg', \
         selector: "topic = 'org.fedoraproject.prod.git.receive'"
    echo "CI_MESSAGE = " + CI_MESSAGE

    scm {
        github('CentOS-PaaS-SIG/ci-pipeline', 'master')
    }

    stage('rpmbuild-trigger')
      sh """{

            set -xuo pipefail

            ls
            ls ci-pipeline

//            # Write script to parse fields (can likely be improved)
//            cat << EOF > ${WORKSPACE}/parse_fedmsg.py
//            #!/bin/env python
//            import json
//            import sys
//
//            reload(sys)
//            sys.setdefaultencoding('utf-8')
//            message = json.load(sys.stdin)
//            if 'commit' in message:
//                msg = message['commit']
//
//                for key in msg:
//                    print "fed_%s=%s" % (key, msg[key])
//            EOF
//            chmod +x ${WORKSPACE}/parse_fedmsg.py
//
//            # Write fedmsg fields to a file to inject them
//            if [ -n "$CI_MESSAGE" ]; then
//                echo $CI_MESSAGE | ${WORKSPACE}/parse_fedmsg.py > fedmsg_fields.txt
//            fi
}"""
}
