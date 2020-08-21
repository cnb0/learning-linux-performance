

##  performance testing early

```

- In today's world, applications for vertical markets, 
        such as insurance, banking, healthcare, retail, and telecommunications, 
        play critical roles in day-to-day transactions. 
        Even the smallest delay in one transaction can impact business growth and stock market value.
        With that in mind, company leaders often ask these questions

- Run performance testing to ensure that your application remains available 
  during critical times by verifying the 
        - responsiveness 
        - throughput 
        - speed
        - reliability 
        - scalability of a system or application under a workload.

        - Can I ensure less than 3-second response times for my critical transactions?
        - How do I achieve the needed throughput for the peak season?
        - How do I build effective, reliable, and resilient IT systems?

- Performance testing can help you answer those questions by verifying the 
        - responsiveness 
        - throughput 
        - speed 
        - reliability 
        - scalability of a system or application under a workload. 
        
         Usually, performance testing is conducted to accomplish these goals:
                   - Evaluate the system against performance criteria
                   - Find the source of performance problems
                   - Support system tuning
                   - Compare the performance characteristics of multiple systems or system configurations
                   - Find throughput levels
                   - Assess production readiness as one of the parameters

- Types of performance tests

        - Typically, a performance test fits into one of these categories:

                - Load testing
                        - determines or validates the performance characteristics of a system or 
                          application under test by subjecting it to the types of workloads and 
                          load volumes that are anticipated during production operations. 
                          The purpose of load testing is to determine whether 
                          the application can handle the expected load.

                - Stress testing 
                        - determines or validates the performance characteristics of the system or 
                          application under test when it is subjected to conditions beyond 
                          what is anticipated during production operations. 
                        - The purpose of stress testing is to find the maximum load that 
                          the system can handle before it breaks.

                - Capacity testing 
                        - tests potential loads that the system might need to support in the future.

                -  Volume testing 
                        - verifies that the performance of the system or 
                        - application isn't affected when it is subjected to the anticipated volumes of data.

                - Endurance testing verifies 
                        - whether the system or application can run well over a period and 
                          identifies potential threats, such as third-party tools or 
                          vendor integrations, that might slow the system.

- Performance testing in practice

        - Performance testing involves these activities:

                  -  Understand the project vision and context. 
                     Identify the implications of performance on the services
                     that the application or system is intended to provide.

                  -  Identify the performance testing objectives. 
                     What are your goals? What value do they add?

                  -  Prepare a performance test strategy.

                  -  Establish the right test environment.

                  -  Identify the performance test acceptance criteria. 
                     For example, 
                             - identify the response time, throughput, and resource utilization goals and 
                             - constraints for your tests. 
                             - In general, 
                                    - response time is a user concern, 
                                    - throughput is a business concern, 
                                    - resource utilization is a system concern.

                  - Plan and design your tests. 
                             - Identify key scenarios, determine variability among representative users and 
                             - how to simulate that variability, 
                             - define test data, and establish metrics that are to be collected. 
                             - Consolidate this information into one or more models of system usage 
                               that can be implemented, run, and analyzed.

                  - Drive automated test loads and run the test.

                  - Identify performance bottlenecks through real-time monitoring and reporting.

                  - Reprioritize and retest.
                        - When all of the metric values are within accepted limits,
                          none of the set thresholds are violated, and all of the information 
                          that you want is collected, you are finished testing that 
                          particular scenario on that particular configuration.

- The benefits of performance testing
            - Including performance testing early in development lifecycle 
              can add significant value to the project. Performance testing can lead to several benefits:
                   - Eliminating late system deployment due to performance issues
                   - Eliminating avoidable system rework due to performance issues
                   - Establishing performance baselines for future testing and service level agreements (SLAs)
                   - Eliminating avoidable system tuning efforts
                   - Reducing operational overhead for handling system issues due to performance problems

- Hints and tips for performance testing

            - When you adopt performance testing practice, keep these tips in mind:

            - Evaluate the performance characteristics of the software system 
              after the functional and system testing is completed.
                     In a highly agile environment, test performance early, during each iteration, and 
                     focus on fixing performance bottlenecks at both the component and application levels:
                            a. Run performance tests on each component level separately and
                               focus on component throughput and concurrency. 
                               Push the system beyond its breaking point and observe the behavior.
                            b. Run performance tests at the application or system level for user experiences 
                               under normal and maximum loads.Capture the performance metrics and 
                               verify that the performance objectives are met